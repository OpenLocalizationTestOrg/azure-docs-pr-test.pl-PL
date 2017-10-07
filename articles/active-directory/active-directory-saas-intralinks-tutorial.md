---
title: 'Samouczek: Integracji Azure Active Directory z Intralinks | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="ff8bd-103">Samouczek: Integracji Azure Active Directory z Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff8bd-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="ff8bd-104">Z tego samouczka, dowiesz się, jak toointegrate Intralinks w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff8bd-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff8bd-105">Integracja z usługą Azure AD Intralinks zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ff8bd-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="ff8bd-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="ff8bd-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIntralinks (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8bd-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff8bd-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ff8bd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ff8bd-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff8bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff8bd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff8bd-110">Prerequisites</span></span>

<span data-ttu-id="ff8bd-111">tooconfigure integracji z usługą Azure AD z Intralinks należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="ff8bd-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff8bd-113">Intralinks logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ff8bd-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff8bd-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff8bd-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff8bd-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff8bd-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff8bd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff8bd-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ff8bd-118">Scenario description</span></span>
<span data-ttu-id="ff8bd-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff8bd-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff8bd-121">Dodawanie Intralinks z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ff8bd-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="ff8bd-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff8bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="ff8bd-123">Dodawanie Intralinks z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ff8bd-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="ff8bd-124">tooconfigure hello integracji Intralinks do usługi Azure AD, należy tooadd Intralinks z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ff8bd-125">**tooadd Intralinks z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff8bd-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff8bd-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ff8bd-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff8bd-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff8bd-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff8bd-133">W polu wyszukiwania hello wpisz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-133">In hello search box, type **Intralinks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff8bd-135">W panelu wyników hello zaznacz **Intralinks**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff8bd-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff8bd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff8bd-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intralinks w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff8bd-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Intralinks jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="ff8bd-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Intralinks musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="ff8bd-141">W Intralinks, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ff8bd-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Intralinks, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ff8bd-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ff8bd-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff8bd-145">**[Tworzenie użytkownika testowego Intralinks](#creating-an-intralinks-test-user)**  -toohave odpowiednikiem Simona Britta w Intralinks, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff8bd-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff8bd-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff8bd-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff8bd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff8bd-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="ff8bd-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Intralinks, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff8bd-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff8bd-151">W portalu Azure na powitania hello **Intralinks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ff8bd-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="ff8bd-155">Na powitania **Intralinks domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="ff8bd-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="ff8bd-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff8bd-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-158">This value is not real.</span></span> <span data-ttu-id="ff8bd-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ff8bd-160">Skontaktuj się z [zespołem pomocy technicznej klienta Intralinks](https://www.intralinks.com/contact-1) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="ff8bd-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="ff8bd-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff8bd-165">tooconfigure rejestracji jednokrotnej w **Intralinks** strony, należy pobrać hello toosend **XML metadanych** [Intralinks obsługuje zespołu](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="ff8bd-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="ff8bd-166">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ff8bd-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ff8bd-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ff8bd-168">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ff8bd-169">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff8bd-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff8bd-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8bd-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff8bd-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ff8bd-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ff8bd-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff8bd-174">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff8bd-176">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff8bd-178">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff8bd-180">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff8bd-182">a.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-182">a.</span></span> <span data-ttu-id="ff8bd-183">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff8bd-184">b.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-184">b.</span></span> <span data-ttu-id="ff8bd-185">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff8bd-186">c.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-186">c.</span></span> <span data-ttu-id="ff8bd-187">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ff8bd-188">d.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-188">d.</span></span> <span data-ttu-id="ff8bd-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="ff8bd-190">Tworzenie użytkownika testowego Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff8bd-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="ff8bd-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="ff8bd-192">We współpracy z [Intralinks obsługuje zespołu](https://www.intralinks.com/contact-1) użytkowników hello tooadd hello Intralinks platformy.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ff8bd-193">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8bd-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ff8bd-194">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIntralinks.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ff8bd-196">**tooassign tooIntralinks Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ff8bd-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff8bd-197">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ff8bd-199">Z listy aplikacji hello wybierz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-199">In hello applications list, select **Intralinks**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="ff8bd-201">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ff8bd-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-203">Click **Add** button.</span></span> <span data-ttu-id="ff8bd-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ff8bd-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ff8bd-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff8bd-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="ff8bd-209">Dodaj aplikację Intralinks za pośrednictwem lub Elite</span><span class="sxs-lookup"><span data-stu-id="ff8bd-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="ff8bd-210">Używa Intralinks hello tę samą platformę tożsamości logowania jednokrotnego dla wszystkich innych aplikacji Intralinks z wyjątkiem aplikacji węzła transakcji.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="ff8bd-211">Dlatego jeśli planujesz toouse inna aplikacja Intralinks następnie najpierw należy tooconfigure logowania jednokrotnego dla jednej aplikacji głównej Intralinks przy użyciu procedury hello opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="ff8bd-212">Po wykonaniu tej można wykonać hello poniżej procedura tooadd inna aplikacja Intralinks w dzierżawie, które mogą korzystać z tej aplikacji głównej dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="ff8bd-213">Ta funkcja jest dostępna tylko klientów SKU Premium tooAzure AD i nie jest dostępna dla klientów bezpłatna lub podstawowy SKU.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="ff8bd-214">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]


2. <span data-ttu-id="ff8bd-216">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff8bd-217">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-217">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff8bd-219">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff8bd-221">W polu wyszukiwania hello wpisz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-221">In hello search box, type **Intralinks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff8bd-223">Na **Intralinks Dodaj aplikację** wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Dodawanie aplikacji Intralinks za pośrednictwem lub Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="ff8bd-225">a.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-225">a.</span></span> <span data-ttu-id="ff8bd-226">W **nazwa** pole tekstowe, np. Wprowadź odpowiednią nazwę aplikacji hello **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="ff8bd-227">b.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-227">b.</span></span> <span data-ttu-id="ff8bd-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="ff8bd-229">W portalu Azure na powitania hello **Intralinks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

7. <span data-ttu-id="ff8bd-231">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **połączonej logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="ff8bd-233">Pobieranie adresu URL logowania jednokrotnego zainicjowano hello SP hello z [zespołu Intralinks](https://www.intralinks.com/contact-1) dla hello inna aplikacja Intralinks i wprowadź go w **Konfiguruj adres URL logowania** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="ff8bd-235">W polu tekstowym na adres URL logowania hello wpisz adres URL hello używanych przez aplikację Intralinks toosign na tooyour użytkowników przy użyciu następującego wzorca hello:</span><span class="sxs-lookup"><span data-stu-id="ff8bd-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="ff8bd-236">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-236">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="ff8bd-238">Przypisz toouser aplikacji hello lub grupy, jak pokazano w sekcji hello  **[użytkownika testowego hello Azure AD przypisywanie](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff8bd-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff8bd-239">Testing single sign-on</span></span>

<span data-ttu-id="ff8bd-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ff8bd-241">Po kliknięciu powitalne Intralinks kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Intralinks aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff8bd-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="ff8bd-242">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff8bd-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff8bd-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ff8bd-243">Additional resources</span></span>

* [<span data-ttu-id="ff8bd-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff8bd-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff8bd-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff8bd-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

