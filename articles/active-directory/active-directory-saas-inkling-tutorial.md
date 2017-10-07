---
title: 'Samouczek: Integracji Azure Active Directory z Inkling | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="11d97-103">Samouczek: Integracji Azure Active Directory z Inkling</span><span class="sxs-lookup"><span data-stu-id="11d97-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="11d97-104">Z tego samouczka, dowiesz się, jak toointegrate Inkling w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11d97-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11d97-105">Integracja z usługą Azure AD Inkling zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="11d97-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11d97-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooInkling</span><span class="sxs-lookup"><span data-stu-id="11d97-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="11d97-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooInkling (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="11d97-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11d97-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="11d97-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="11d97-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11d97-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11d97-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="11d97-110">Prerequisites</span></span>

<span data-ttu-id="11d97-111">tooconfigure integracji z usługą Azure AD z Inkling należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="11d97-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="11d97-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="11d97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11d97-113">Inkling jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="11d97-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="11d97-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="11d97-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="11d97-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="11d97-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11d97-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="11d97-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="11d97-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11d97-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="11d97-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="11d97-118">Scenario description</span></span>
<span data-ttu-id="11d97-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="11d97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11d97-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="11d97-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11d97-121">Dodawanie Inkling z galerii hello</span><span class="sxs-lookup"><span data-stu-id="11d97-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="11d97-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="11d97-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="11d97-123">Dodawanie Inkling z galerii hello</span><span class="sxs-lookup"><span data-stu-id="11d97-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="11d97-124">tooconfigure hello integracji Inkling do usługi Azure AD, należy tooadd Inkling z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="11d97-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11d97-125">**tooadd Inkling z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11d97-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d97-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="11d97-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="11d97-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="11d97-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11d97-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="11d97-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="11d97-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="11d97-133">W polu wyszukiwania hello wpisz **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="11d97-133">In hello search box, type **Inkling**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="11d97-135">W panelu wyników hello zaznacz **Inkling**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="11d97-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11d97-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="11d97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11d97-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Inkling w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11d97-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Inkling jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11d97-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="11d97-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Inkling musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="11d97-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="11d97-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Inkling.</span><span class="sxs-lookup"><span data-stu-id="11d97-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="11d97-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Inkling, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="11d97-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11d97-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="11d97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11d97-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="11d97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11d97-145">**[Tworzenie użytkownika testowego Inkling](#creating-an-inkling-test-user)**  -toohave odpowiednikiem Simona Britta w Inkling, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11d97-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="11d97-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="11d97-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11d97-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="11d97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11d97-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="11d97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11d97-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Inkling.</span><span class="sxs-lookup"><span data-stu-id="11d97-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="11d97-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Inkling, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11d97-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d97-151">W portalu zarządzania Azure hello na powitania **Inkling** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="11d97-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="11d97-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="11d97-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="11d97-155">Na powitania **Inkling domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="11d97-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="11d97-157">a.</span><span class="sxs-lookup"><span data-stu-id="11d97-157">a.</span></span> <span data-ttu-id="11d97-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="11d97-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="11d97-159">b.</span><span class="sxs-lookup"><span data-stu-id="11d97-159">b.</span></span> <span data-ttu-id="11d97-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="11d97-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11d97-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="11d97-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="11d97-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="11d97-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="11d97-163">Skontaktuj się z [zespołem pomocy technicznej Inkling](mailto:press@inkling.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="11d97-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="11d97-164">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="11d97-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="11d97-166">Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="11d97-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="11d97-167">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="11d97-167">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="11d97-169">Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="11d97-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="11d97-171">W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="11d97-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="11d97-173">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="11d97-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="11d97-175">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej Inkling](mailto:press@inkling.com) i udostępniać je z pobrane **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="11d97-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11d97-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="11d97-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="11d97-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="11d97-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="11d97-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11d97-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d97-180">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="11d97-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11d97-182">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="11d97-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11d97-184">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11d97-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="11d97-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11d97-188">a.</span><span class="sxs-lookup"><span data-stu-id="11d97-188">a.</span></span> <span data-ttu-id="11d97-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11d97-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11d97-190">b.</span><span class="sxs-lookup"><span data-stu-id="11d97-190">b.</span></span> <span data-ttu-id="11d97-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11d97-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11d97-192">c.</span><span class="sxs-lookup"><span data-stu-id="11d97-192">c.</span></span> <span data-ttu-id="11d97-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="11d97-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11d97-194">d.</span><span class="sxs-lookup"><span data-stu-id="11d97-194">d.</span></span> <span data-ttu-id="11d97-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="11d97-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="11d97-196">Tworzenie użytkownika testowego Inkling</span><span class="sxs-lookup"><span data-stu-id="11d97-196">Creating an Inkling test user</span></span>

<span data-ttu-id="11d97-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Inkling.</span><span class="sxs-lookup"><span data-stu-id="11d97-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="11d97-198">We współpracy z [zespołem pomocy technicznej Inkling](mailto:press@inkling.com) tooadd hello użytkowników hello Inkling platformy.</span><span class="sxs-lookup"><span data-stu-id="11d97-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11d97-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="11d97-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11d97-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooInkling dostępu.</span><span class="sxs-lookup"><span data-stu-id="11d97-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="11d97-202">**tooassign tooInkling Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="11d97-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d97-203">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="11d97-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="11d97-205">Z listy aplikacji hello wybierz **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="11d97-205">In hello applications list, select **Inkling**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="11d97-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="11d97-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="11d97-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="11d97-209">Click **Add** button.</span></span> <span data-ttu-id="11d97-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="11d97-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="11d97-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11d97-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11d97-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11d97-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="11d97-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="11d97-215">Testing single sign-on</span></span>

<span data-ttu-id="11d97-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="11d97-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11d97-217">Po kliknięciu kafelka Inkling hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Inkling aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11d97-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="11d97-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="11d97-218">Additional resources</span></span>

* [<span data-ttu-id="11d97-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11d97-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11d97-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11d97-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png