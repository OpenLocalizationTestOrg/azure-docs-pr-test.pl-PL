---
title: 'Samouczek: Integracji Azure Active Directory z Fuze | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="cf6b5-103">Samouczek: Integracji Azure Active Directory z Fuze</span><span class="sxs-lookup"><span data-stu-id="cf6b5-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="cf6b5-104">Z tego samouczka, dowiesz się, jak toointegrate Fuze z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf6b5-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf6b5-105">Integracja z usługą Azure AD Fuze zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf6b5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFuze</span><span class="sxs-lookup"><span data-stu-id="cf6b5-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="cf6b5-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFuze (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6b5-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf6b5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="cf6b5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cf6b5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf6b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf6b5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf6b5-110">Prerequisites</span></span>

<span data-ttu-id="cf6b5-111">tooconfigure integracji z usługą Azure AD z Fuze należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="cf6b5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf6b5-113">Fuze jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cf6b5-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="cf6b5-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cf6b5-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf6b5-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cf6b5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf6b5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cf6b5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cf6b5-118">Scenario description</span></span>
<span data-ttu-id="cf6b5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf6b5-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf6b5-121">Dodawanie Fuze z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cf6b5-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="cf6b5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cf6b5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="cf6b5-123">Dodawanie Fuze z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cf6b5-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="cf6b5-124">tooconfigure hello integracji Fuze do usługi Azure AD, należy tooadd Fuze z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf6b5-125">**tooadd Fuze z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cf6b5-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6b5-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cf6b5-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf6b5-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cf6b5-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cf6b5-133">W polu wyszukiwania hello wpisz **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-133">In hello search box, type **Fuze**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="cf6b5-135">W panelu wyników hello zaznacz **Fuze**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf6b5-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cf6b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf6b5-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Fuze w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf6b5-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Fuze jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="cf6b5-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Fuze musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="cf6b5-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Fuze.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="cf6b5-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Fuze, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf6b5-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf6b5-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf6b5-145">**[Tworzenie użytkownika testowego Fuze](#creating-a-fuze-test-user)**  -toohave odpowiednikiem Simona Britta w Fuze, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cf6b5-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf6b5-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf6b5-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cf6b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf6b5-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Fuze.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="cf6b5-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Fuze, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cf6b5-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6b5-151">W portalu zarządzania Azure hello na powitania **Fuze** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cf6b5-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="cf6b5-155">Na powitania **Fuze domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="cf6b5-157">W hello **Zaloguj się na adres URL** pole tekstowe, wprowadź adres URL hello logowania jako:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="cf6b5-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="cf6b5-158">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-158">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="cf6b5-160">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik xml hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="cf6b5-162">tooconfigure rejestracji jednokrotnej w **Fuze** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="cf6b5-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="cf6b5-163">One będzie skonfigurowanie tego numeru w kolejności toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf6b5-164">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6b5-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf6b5-165">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cf6b5-167">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cf6b5-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6b5-168">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf6b5-170">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf6b5-172">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf6b5-174">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cf6b5-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf6b5-176">a.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-176">a.</span></span> <span data-ttu-id="cf6b5-177">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf6b5-178">b.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-178">b.</span></span> <span data-ttu-id="cf6b5-179">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf6b5-180">c.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-180">c.</span></span> <span data-ttu-id="cf6b5-181">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf6b5-182">d.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-182">d.</span></span> <span data-ttu-id="cf6b5-183">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="cf6b5-184">Tworzenie użytkownika testowego Fuze</span><span class="sxs-lookup"><span data-stu-id="cf6b5-184">Creating a Fuze test user</span></span>

<span data-ttu-id="cf6b5-185">Aplikacja fuze obsługuje zaraz pełna rezerw użytkownika czasu, użytkownicy będą tworzone automatycznie podczas ich logowania.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="cf6b5-186">Dla innych wyjaśnienie, skontaktuj się z Fuze [obsługuje](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="cf6b5-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf6b5-187">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6b5-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf6b5-188">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooFuze dostępu.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cf6b5-190">**tooassign tooFuze Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cf6b5-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6b5-191">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cf6b5-193">Z listy aplikacji hello wybierz **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-193">In hello applications list, select **Fuze**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="cf6b5-195">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cf6b5-197">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-197">Click **Add** button.</span></span> <span data-ttu-id="cf6b5-198">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cf6b5-200">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf6b5-201">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf6b5-202">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="cf6b5-203">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cf6b5-203">Testing single sign-on</span></span>

<span data-ttu-id="cf6b5-204">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf6b5-205">Po kliknięciu kafelka Fuze hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Fuze aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cf6b5-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cf6b5-206">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cf6b5-206">Additional resources</span></span>

* [<span data-ttu-id="cf6b5-207">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf6b5-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf6b5-208">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf6b5-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png