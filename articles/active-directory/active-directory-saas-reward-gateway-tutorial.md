---
title: "Samouczek: Integracja usługi Azure Active Directory z bramą opłatą | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i bramą osób trzecich."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 30cdd538471b373468c3d990e4568ddb08081a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="9abfc-103">Samouczek: Integracja usługi Azure Active Directory z bramą osób trzecich</span><span class="sxs-lookup"><span data-stu-id="9abfc-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="9abfc-104">Z tego samouczka, dowiesz się, jak toointegrate wynagrodzenie bramy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9abfc-104">In this tutorial, you learn how toointegrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9abfc-105">Integrowanie opłatą bramy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9abfc-105">Integrating Reward Gateway with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9abfc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooReward bramy</span><span class="sxs-lookup"><span data-stu-id="9abfc-106">You can control in Azure AD who has access tooReward Gateway</span></span>
- <span data-ttu-id="9abfc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooReward bramy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9abfc-107">You can enable your users tooautomatically get signed-on tooReward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9abfc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9abfc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9abfc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9abfc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9abfc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9abfc-110">Prerequisites</span></span>

<span data-ttu-id="9abfc-111">tooconfigure Integracja usługi Azure AD z bramą wynagrodzenie, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9abfc-111">tooconfigure Azure AD integration with Reward Gateway, you need hello following items:</span></span>

- <span data-ttu-id="9abfc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9abfc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9abfc-113">Bramy opłatą logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9abfc-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9abfc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9abfc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9abfc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9abfc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9abfc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9abfc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9abfc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9abfc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9abfc-118">Scenario description</span></span>
<span data-ttu-id="9abfc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9abfc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9abfc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9abfc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9abfc-121">Dodawanie opłatą bramy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9abfc-121">Adding Reward Gateway from hello gallery</span></span>
2. <span data-ttu-id="9abfc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9abfc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-hello-gallery"></a><span data-ttu-id="9abfc-123">Dodawanie opłatą bramy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9abfc-123">Adding Reward Gateway from hello gallery</span></span>
<span data-ttu-id="9abfc-124">tooconfigure hello integracji opłatą bramy w usłudze Azure Active Directory, należy tooadd wynagrodzenie bramy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9abfc-124">tooconfigure hello integration of Reward Gateway into Azure AD, you need tooadd Reward Gateway from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9abfc-125">**tooadd wynagrodzenie bramy z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9abfc-125">**tooadd Reward Gateway from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9abfc-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9abfc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9abfc-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9abfc-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9abfc-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9abfc-133">W polu wyszukiwania hello wpisz **bramy opłatą**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-133">In hello search box, type **Reward Gateway**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="9abfc-135">W panelu wyników hello, wybierz **wynagrodzenie bramy**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9abfc-135">In hello results panel, select **Reward Gateway**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9abfc-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9abfc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9abfc-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z bramą osób trzecich, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9abfc-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9abfc-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello opłatą bramy jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9abfc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Reward Gateway is tooa user in Azure AD.</span></span> <span data-ttu-id="9abfc-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi opłatą bramy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9abfc-140">In other words, a link relationship between an Azure AD user and hello related user in Reward Gateway needs toobe established.</span></span>

<span data-ttu-id="9abfc-141">W polu Brama wynagrodzenie, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9abfc-141">In Reward Gateway, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9abfc-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z bramą wynagrodzenie, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9abfc-142">tooconfigure and test Azure AD single sign-on with Reward Gateway, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9abfc-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9abfc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9abfc-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9abfc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9abfc-145">**[Tworzenie użytkownika testowego bramy opłatą](#creating-a-reward-gateway-test-user)**  -toohave odpowiednikiem Simona Britta bramy osób trzecich, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9abfc-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - toohave a counterpart of Britta Simon in Reward Gateway that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9abfc-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9abfc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9abfc-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9abfc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9abfc-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9abfc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9abfc-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji bramy osób trzecich.</span><span class="sxs-lookup"><span data-stu-id="9abfc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="9abfc-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z bramą wynagrodzenie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9abfc-150">**tooconfigure Azure AD single sign-on with Reward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="9abfc-151">W portalu Azure na powitania hello **bramy opłatą** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-151">In hello Azure portal, on hello **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9abfc-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9abfc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="9abfc-155">Na powitania **domeny bramy opłatą i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9abfc-155">On hello **Reward Gateway Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="9abfc-157">a.</span><span class="sxs-lookup"><span data-stu-id="9abfc-157">a.</span></span> <span data-ttu-id="9abfc-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="9abfc-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="9abfc-159">b.</span><span class="sxs-lookup"><span data-stu-id="9abfc-159">b.</span></span> <span data-ttu-id="9abfc-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="9abfc-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="9abfc-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9abfc-161">These values are not real.</span></span> <span data-ttu-id="9abfc-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9abfc-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9abfc-163">Skontaktuj się z [zespołem pomocy technicznej bramy opłatą](mailto:clientsupport@rewardgateway.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9abfc-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) tooget these values.</span></span>
 
4. <span data-ttu-id="9abfc-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9abfc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="9abfc-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9abfc-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9abfc-168">tooconfigure rejestracji jednokrotnej w **wynagrodzenie bramy** strony, należy pobrać hello toosend **XML metadanych** zbyt[zespołem pomocy technicznej bramy opłatą](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="9abfc-168">tooconfigure single sign-on on **Reward Gateway** side, you need toosend hello downloaded **Metadata XML** too[Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="9abfc-169">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="9abfc-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9abfc-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9abfc-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9abfc-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9abfc-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9abfc-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9abfc-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9abfc-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9abfc-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="9abfc-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9abfc-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9abfc-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9abfc-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9abfc-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9abfc-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9abfc-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9abfc-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9abfc-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9abfc-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9abfc-185">a.</span><span class="sxs-lookup"><span data-stu-id="9abfc-185">a.</span></span> <span data-ttu-id="9abfc-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9abfc-187">b.</span><span class="sxs-lookup"><span data-stu-id="9abfc-187">b.</span></span> <span data-ttu-id="9abfc-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9abfc-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9abfc-189">c.</span><span class="sxs-lookup"><span data-stu-id="9abfc-189">c.</span></span> <span data-ttu-id="9abfc-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9abfc-191">d.</span><span class="sxs-lookup"><span data-stu-id="9abfc-191">d.</span></span> <span data-ttu-id="9abfc-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="9abfc-193">Tworzenie użytkownika testowego bramy osób trzecich</span><span class="sxs-lookup"><span data-stu-id="9abfc-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="9abfc-194">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w bramy osób trzecich.</span><span class="sxs-lookup"><span data-stu-id="9abfc-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="9abfc-195">Praca z bramą osób trzecich [zespołu obsługi](mailto:clientsupport@rewardgateway.com) użytkowników hello tooadd hello bramy opłatą platformy.</span><span class="sxs-lookup"><span data-stu-id="9abfc-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) tooadd hello users in hello Reward Gateway platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9abfc-196">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9abfc-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9abfc-197">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooReward bramy.</span><span class="sxs-lookup"><span data-stu-id="9abfc-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooReward Gateway.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9abfc-199">**tooassign tooReward Simona Britta bramy, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9abfc-199">**tooassign Britta Simon tooReward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="9abfc-200">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9abfc-202">Z listy aplikacji hello wybierz **bramy opłatą**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-202">In hello applications list, select **Reward Gateway**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="9abfc-204">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9abfc-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9abfc-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9abfc-206">Click **Add** button.</span></span> <span data-ttu-id="9abfc-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9abfc-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9abfc-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9abfc-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9abfc-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9abfc-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9abfc-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9abfc-212">Testing single sign-on</span></span>

<span data-ttu-id="9abfc-213">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9abfc-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9abfc-214">Po kliknięciu kafelka bramy opłatą hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour wynagrodzenie bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9abfc-214">When you click hello Reward Gateway tile in hello Access Panel, you should get automatically signed-on tooyour Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9abfc-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9abfc-215">Additional resources</span></span>

* [<span data-ttu-id="9abfc-216">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9abfc-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9abfc-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9abfc-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

