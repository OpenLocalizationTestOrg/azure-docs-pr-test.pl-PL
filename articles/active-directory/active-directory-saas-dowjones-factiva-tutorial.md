---
title: 'Samouczek: Integracji Azure Active Directory z Factiva Nowak knie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Factiva Nowak knie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c42b5d64433c7bdcb512771a3e68115cc5f6874
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="3462c-103">Samouczek: Integracji Azure Active Directory z Factiva Nowak knie</span><span class="sxs-lookup"><span data-stu-id="3462c-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="3462c-104">Z tego samouczka, dowiesz się, jak toointegrate Factiva Nowak knie w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3462c-104">In this tutorial, you learn how toointegrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3462c-105">Integracja z usługą Azure AD Factiva Nowak knie zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3462c-105">Integrating Dow Jones Factiva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3462c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooDow Factiva Kowalski</span><span class="sxs-lookup"><span data-stu-id="3462c-106">You can control in Azure AD who has access tooDow Jones Factiva</span></span>
- <span data-ttu-id="3462c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDow Factiva Nowak (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3462c-107">You can enable your users tooautomatically get signed-on tooDow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3462c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3462c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3462c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3462c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3462c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3462c-110">Prerequisites</span></span>

<span data-ttu-id="3462c-111">tooconfigure integracji usługi Azure AD z Factiva Nowak knie należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3462c-111">tooconfigure Azure AD integration with Dow Jones Factiva, you need hello following items:</span></span>

- <span data-ttu-id="3462c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3462c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3462c-113">Knie Nowak Factiva jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3462c-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3462c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3462c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3462c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3462c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3462c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3462c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3462c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3462c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3462c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3462c-118">Scenario description</span></span>
<span data-ttu-id="3462c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3462c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3462c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3462c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3462c-121">Dodawanie Factiva Nowak knie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3462c-121">Adding Dow Jones Factiva from hello gallery</span></span>
2. <span data-ttu-id="3462c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3462c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-hello-gallery"></a><span data-ttu-id="3462c-123">Dodawanie Factiva Nowak knie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3462c-123">Adding Dow Jones Factiva from hello gallery</span></span>
<span data-ttu-id="3462c-124">tooconfigure hello integracji Factiva Nowak knie do usługi Azure AD, należy tooadd Factiva Nowak knie z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3462c-124">tooconfigure hello integration of Dow Jones Factiva into Azure AD, you need tooadd Dow Jones Factiva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3462c-125">**tooadd Factiva Nowak knie z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3462c-125">**tooadd Dow Jones Factiva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3462c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3462c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3462c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3462c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3462c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3462c-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3462c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3462c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3462c-133">W polu wyszukiwania hello wpisz **knie Nowak Factiva**.</span><span class="sxs-lookup"><span data-stu-id="3462c-133">In hello search box, type **Dow Jones Factiva**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="3462c-135">W panelu wyników hello, wybierz **Factiva Nowak knie**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3462c-135">In hello results panel, select **Dow Jones Factiva**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3462c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3462c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3462c-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="3462c-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3462c-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Factiva Nowak knie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3462c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dow Jones Factiva is tooa user in Azure AD.</span></span> <span data-ttu-id="3462c-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w knie Factiva Nowak musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="3462c-140">In other words, a link relationship between an Azure AD user and hello related user in Dow Jones Factiva needs toobe established.</span></span>

<span data-ttu-id="3462c-141">W knie Nowak Factiva, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="3462c-141">In Dow Jones Factiva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3462c-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="3462c-142">tooconfigure and test Azure AD single sign-on with Dow Jones Factiva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3462c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3462c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3462c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3462c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3462c-145">**[Tworzenie użytkownika testowego Factiva Nowak knie](#creating-a-dow-jones-factiva-test-user)**  -toohave odpowiednikiem Simona Britta w Factiva Nowak knie, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3462c-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - toohave a counterpart of Britta Simon in Dow Jones Factiva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3462c-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3462c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3462c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="3462c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3462c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3462c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3462c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="3462c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="3462c-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3462c-150">**tooconfigure Azure AD single sign-on with Dow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="3462c-151">W portalu Azure na powitania hello **Factiva Nowak knie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3462c-151">In hello Azure portal, on hello **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3462c-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3462c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="3462c-155">Na powitania **knie Nowak Factiva domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="3462c-155">On hello **Dow Jones Factiva Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="3462c-157">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3462c-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="3462c-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3462c-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3462c-161">tooconfigure rejestracji jednokrotnej w **Factiva Nowak knie** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Factiva Nowak knie](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="3462c-161">tooconfigure single sign-on on **Dow Jones Factiva** side, you need toosend hello downloaded **Metadata XML** too[Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="3462c-162">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="3462c-162">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3462c-163">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="3462c-163">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3462c-164">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="3462c-164">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3462c-165">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3462c-165">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3462c-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3462c-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="3462c-167">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="3462c-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3462c-169">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3462c-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3462c-170">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3462c-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3462c-172">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3462c-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3462c-174">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3462c-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3462c-176">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3462c-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3462c-178">a.</span><span class="sxs-lookup"><span data-stu-id="3462c-178">a.</span></span> <span data-ttu-id="3462c-179">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3462c-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3462c-180">b.</span><span class="sxs-lookup"><span data-stu-id="3462c-180">b.</span></span> <span data-ttu-id="3462c-181">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3462c-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3462c-182">c.</span><span class="sxs-lookup"><span data-stu-id="3462c-182">c.</span></span> <span data-ttu-id="3462c-183">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3462c-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3462c-184">d.</span><span class="sxs-lookup"><span data-stu-id="3462c-184">d.</span></span> <span data-ttu-id="3462c-185">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3462c-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="3462c-186">Tworzenie użytkownika testowego Factiva Nowak knie</span><span class="sxs-lookup"><span data-stu-id="3462c-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="3462c-187">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="3462c-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="3462c-188">We współpracy z knie [zespołem pomocy technicznej Factiva Nowak](https://www.dowjones.com/contact/) użytkowników hello tooadd hello Factiva Nowak knie platformy.</span><span class="sxs-lookup"><span data-stu-id="3462c-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) tooadd hello users in hello Dow Jones Factiva platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3462c-189">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3462c-189">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3462c-190">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDow Factiva Nowak.</span><span class="sxs-lookup"><span data-stu-id="3462c-190">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDow Jones Factiva.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3462c-192">**tooassign tooDow Simona Britta Factiva Nowak wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3462c-192">**tooassign Britta Simon tooDow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="3462c-193">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3462c-193">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3462c-195">Z listy aplikacji hello wybierz **knie Nowak Factiva**.</span><span class="sxs-lookup"><span data-stu-id="3462c-195">In hello applications list, select **Dow Jones Factiva**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="3462c-197">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3462c-197">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3462c-199">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3462c-199">Click **Add** button.</span></span> <span data-ttu-id="3462c-200">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3462c-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3462c-202">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3462c-202">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3462c-203">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3462c-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3462c-204">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3462c-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3462c-205">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3462c-205">Testing single sign-on</span></span>

<span data-ttu-id="3462c-206">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3462c-206">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3462c-207">Po kliknięciu kafelka Factiva Nowak knie hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Factiva Nowak knie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3462c-207">When you click hello Dow Jones Factiva tile in hello Access Panel, you should get automatically signed-on tooyour Dow Jones Factiva application.</span></span>
<span data-ttu-id="3462c-208">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3462c-208">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3462c-209">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3462c-209">Additional resources</span></span>

* [<span data-ttu-id="3462c-210">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3462c-210">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3462c-211">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3462c-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

