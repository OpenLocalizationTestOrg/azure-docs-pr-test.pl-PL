---
title: "Samouczek: Integracji Azure Active Directory ze wskazówkami firmy Microsoft | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i wskazówkami w systemie Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 59a8b856fd2dc75a37e9bb8f46ced066bcd0fd56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="b67de-103">Samouczek: Integracji Azure Active Directory ze wskazówkami firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="b67de-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="b67de-104">Z tego samouczka, dowiesz się, jak toointegrate kierunkach firmy Microsoft w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b67de-104">In this tutorial, you learn how toointegrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b67de-105">Integracja z usługą Azure AD instrukcjami w systemie Microsoft udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b67de-105">Integrating Directions on Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b67de-106">Można kontrolować w usłudze Azure AD mającego tooDirections dostępu w systemie Microsoft</span><span class="sxs-lookup"><span data-stu-id="b67de-106">You can control in Azure AD who has access tooDirections on Microsoft</span></span>
- <span data-ttu-id="b67de-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDirections Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67de-107">You can enable your users tooautomatically get signed-on tooDirections on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b67de-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b67de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b67de-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b67de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b67de-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b67de-110">Prerequisites</span></span>

<span data-ttu-id="b67de-111">tooconfigure integracji z usługą Azure AD ze wskazówkami firmy Microsoft, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b67de-111">tooconfigure Azure AD integration with Directions on Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="b67de-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b67de-113">Wskazówki na Microsoft logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b67de-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b67de-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b67de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b67de-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b67de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b67de-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b67de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b67de-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b67de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b67de-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b67de-118">Scenario description</span></span>
<span data-ttu-id="b67de-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b67de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b67de-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b67de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b67de-121">Dodawanie kierunkach Microsoft hello galerii</span><span class="sxs-lookup"><span data-stu-id="b67de-121">Adding Directions on Microsoft from hello gallery</span></span>
2. <span data-ttu-id="b67de-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b67de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-hello-gallery"></a><span data-ttu-id="b67de-123">Dodawanie kierunkach Microsoft hello galerii</span><span class="sxs-lookup"><span data-stu-id="b67de-123">Adding Directions on Microsoft from hello gallery</span></span>
<span data-ttu-id="b67de-124">integracji hello tooconfigure kierunkach firmy Microsoft do usługi Azure AD, należy tooadd kierunkach firmy Microsoft z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b67de-124">tooconfigure hello integration of Directions on Microsoft into Azure AD, you need tooadd Directions on Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b67de-125">**tooadd kierunkach firmy Microsoft z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b67de-125">**tooadd Directions on Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67de-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b67de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b67de-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b67de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b67de-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b67de-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b67de-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b67de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b67de-133">W polu wyszukiwania hello wpisz **kierunkach Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="b67de-133">In hello search box, type **Directions on Microsoft**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="b67de-135">W panelu wyników hello, wybierz **kierunkach Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b67de-135">In hello results panel, select **Directions on Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b67de-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b67de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b67de-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b67de-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b67de-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w kierunkach firmy Microsoft jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Directions on Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="b67de-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w kierunkach Microsoft musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b67de-140">In other words, a link relationship between an Azure AD user and hello related user in Directions on Microsoft needs toobe established.</span></span>

<span data-ttu-id="b67de-141">W kierunkach firmy Microsoft, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b67de-141">In Directions on Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b67de-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b67de-142">tooconfigure and test Azure AD single sign-on with Directions on Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b67de-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b67de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b67de-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b67de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b67de-145">**[Tworzenie kierunki na użytkownika testowego Microsoft](#creating-a-directions-on-microsoft-test-user)**  -toohave odpowiednikiem Simona Britta w kierunkach firmy Microsoft, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b67de-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - toohave a counterpart of Britta Simon in Directions on Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b67de-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b67de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b67de-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b67de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b67de-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b67de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b67de-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestrację jednokrotną w sieci kierunkach aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b67de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="b67de-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej ze wskazówkami firmy Microsoft, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b67de-150">**tooconfigure Azure AD single sign-on with Directions on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67de-151">W portalu Azure na powitania hello **kierunkach Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b67de-151">In hello Azure portal, on hello **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b67de-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b67de-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="b67de-155">Na powitania **kierunkach adresy URL i Domain Microsoft** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b67de-155">On hello **Directions on Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="b67de-157">a.</span><span class="sxs-lookup"><span data-stu-id="b67de-157">a.</span></span> <span data-ttu-id="b67de-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b67de-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="b67de-159">b.</span><span class="sxs-lookup"><span data-stu-id="b67de-159">b.</span></span> <span data-ttu-id="b67de-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b67de-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="b67de-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b67de-161">These values are not real.</span></span> <span data-ttu-id="b67de-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="b67de-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b67de-163">Skontaktuj się z [zespołu obsługi kierunkach Microsoft Client](mailto:service@DirectionsOnMicrosoft.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b67de-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="b67de-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b67de-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="b67de-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b67de-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b67de-168">tooconfigure rejestracji jednokrotnej w **kierunkach Microsoft** strony, należy pobrać hello toosend **XML metadanych** za[kierunkach Microsoft obsługują zespołu](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b67de-168">tooconfigure single sign-on on **Directions on Microsoft** side, you need toosend hello downloaded **Metadata XML** too[Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="b67de-169">tooenable hello kierunkach Microsoft obsługi toolocate zespołu członkostwem w witrynie federacyjnych, zawierają informacje o Twojej firmie w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b67de-169">tooenable hello Directions on Microsoft support team toolocate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="b67de-170">Logowanie jednokrotne dla kierunkach firmy Microsoft wymaga toobe włączane przez hello [kierunkach Microsoft Client obsługuje zespołu](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b67de-170">Single sign-on for Directions on Microsoft needs toobe enabled by hello [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="b67de-171">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona.</span><span class="sxs-lookup"><span data-stu-id="b67de-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="b67de-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b67de-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b67de-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b67de-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b67de-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b67de-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b67de-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67de-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="b67de-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b67de-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b67de-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b67de-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67de-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b67de-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b67de-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b67de-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b67de-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b67de-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b67de-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b67de-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b67de-187">a.</span><span class="sxs-lookup"><span data-stu-id="b67de-187">a.</span></span> <span data-ttu-id="b67de-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b67de-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b67de-189">b.</span><span class="sxs-lookup"><span data-stu-id="b67de-189">b.</span></span> <span data-ttu-id="b67de-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b67de-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b67de-191">c.</span><span class="sxs-lookup"><span data-stu-id="b67de-191">c.</span></span> <span data-ttu-id="b67de-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b67de-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b67de-193">d.</span><span class="sxs-lookup"><span data-stu-id="b67de-193">d.</span></span> <span data-ttu-id="b67de-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b67de-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="b67de-195">Tworzenie kierunki na użytkownika testowego firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="b67de-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="b67de-196">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooDirections w systemie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b67de-196">There is no action item for you tooconfigure user provisioning tooDirections on Microsoft.</span></span>  

<span data-ttu-id="b67de-197">Gdy przypisany użytkownik podejmie próbę toolog w tooDirections w systemie Microsoft za pomocą panelu dostępu hello, kierunkach Microsoft sprawdza, czy użytkownik hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="b67de-197">When an assigned user tries toolog in tooDirections on Microsoft using hello access panel, Directions on Microsoft checks whether hello user exists.</span></span> <span data-ttu-id="b67de-198">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez kierunkach firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b67de-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b67de-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67de-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b67de-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDirections w systemie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b67de-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirections on Microsoft.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b67de-202">**tooassign tooDirections Simona Britta na firmy Microsoft, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b67de-202">**tooassign Britta Simon tooDirections on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="b67de-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b67de-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b67de-205">Z listy aplikacji hello wybierz **kierunkach Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="b67de-205">In hello applications list, select **Directions on Microsoft**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="b67de-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b67de-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b67de-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b67de-209">Click **Add** button.</span></span> <span data-ttu-id="b67de-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b67de-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b67de-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b67de-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b67de-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b67de-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b67de-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b67de-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b67de-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b67de-215">Testing single sign-on</span></span>

<span data-ttu-id="b67de-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b67de-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="b67de-217">Po kliknięciu kierunki hello na kafelku firmy Microsoft w panelu dostępu hello, należy pobrać kierunki automatycznie zalogowane tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b67de-217">When you click hello Directions on Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Directions on Microsoft application.</span></span>

<span data-ttu-id="b67de-218">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b67de-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b67de-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b67de-219">Additional resources</span></span>

* [<span data-ttu-id="b67de-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b67de-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b67de-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b67de-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

