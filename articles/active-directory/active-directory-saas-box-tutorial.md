---
title: 'Samouczek: Integracji Azure Active Directory z polem | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i pola."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="b3589-103">Samouczek: Integracji Azure Active Directory z polem</span><span class="sxs-lookup"><span data-stu-id="b3589-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="b3589-104">Z tego samouczka, dowiesz się, jak pole toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3589-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3589-105">Integracja z usługą Azure AD pole zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b3589-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3589-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBox</span><span class="sxs-lookup"><span data-stu-id="b3589-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="b3589-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBox (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3589-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3589-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b3589-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b3589-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3589-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3589-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3589-110">Prerequisites</span></span>

<span data-ttu-id="b3589-111">tooconfigure integracji z usługą Azure AD z polem należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b3589-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="b3589-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3589-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3589-113">Pole jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3589-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3589-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3589-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3589-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b3589-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3589-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b3589-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3589-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3589-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3589-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b3589-118">Scenario description</span></span>
<span data-ttu-id="b3589-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b3589-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3589-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b3589-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3589-121">Dodawanie pola z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3589-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="b3589-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3589-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="b3589-123">Dodawanie pola z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3589-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="b3589-124">tooconfigure hello integracji pola do usługi Azure AD, należy tooadd pole z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3589-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3589-125">**tooadd pole z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b3589-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3589-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3589-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b3589-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b3589-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3589-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3589-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b3589-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3589-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b3589-133">W polu wyszukiwania hello wpisz **pole**.</span><span class="sxs-lookup"><span data-stu-id="b3589-133">In hello search box, type **Box**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="b3589-135">W panelu wyników hello, wybierz **pole**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b3589-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3589-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3589-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3589-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z polem oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b3589-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3589-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w polu jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3589-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="b3589-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w polu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b3589-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="b3589-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w polu.</span><span class="sxs-lookup"><span data-stu-id="b3589-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="b3589-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z polem, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b3589-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3589-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3589-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3589-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3589-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3589-145">**[Tworzenie użytkownika testowego pole](#creating-a-box-test-user)**  -toohave odpowiednikiem Simona Britta w polu reprezentacja toohello połączonej usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3589-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3589-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3589-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3589-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b3589-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3589-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3589-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3589-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji pole.</span><span class="sxs-lookup"><span data-stu-id="b3589-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="b3589-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z polem, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3589-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3589-151">W portalu Azure na powitania hello **pole** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b3589-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b3589-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3589-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="b3589-155">Na powitania **pole domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b3589-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="b3589-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="b3589-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3589-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b3589-158">This value is not real.</span></span> <span data-ttu-id="b3589-159">Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b3589-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="b3589-160">Skontaktuj się z [zespołem pomocy technicznej klienta pole](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="b3589-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="b3589-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3589-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="b3589-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3589-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3589-165">tooget skonfigurowany dla aplikacji, skontaktuj się z logowania jednokrotnego [zespołem pomocy technicznej klienta pole](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) i dostarczać hello pobrany plik XML.</span><span class="sxs-lookup"><span data-stu-id="b3589-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="b3589-166">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b3589-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3589-167">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b3589-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3589-168">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3589-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3589-169">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3589-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3589-170">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b3589-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b3589-172">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3589-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3589-173">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3589-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3589-175">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b3589-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3589-177">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3589-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3589-179">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b3589-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3589-181">a.</span><span class="sxs-lookup"><span data-stu-id="b3589-181">a.</span></span> <span data-ttu-id="b3589-182">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3589-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3589-183">b.</span><span class="sxs-lookup"><span data-stu-id="b3589-183">b.</span></span> <span data-ttu-id="b3589-184">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b3589-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3589-185">c.</span><span class="sxs-lookup"><span data-stu-id="b3589-185">c.</span></span> <span data-ttu-id="b3589-186">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b3589-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3589-187">d.</span><span class="sxs-lookup"><span data-stu-id="b3589-187">d.</span></span> <span data-ttu-id="b3589-188">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3589-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="b3589-189">Tworzenie użytkownika testowego pole</span><span class="sxs-lookup"><span data-stu-id="b3589-189">Creating a Box test user</span></span>

<span data-ttu-id="b3589-190">W tej sekcji tworzenia użytkownika o nazwie Simona Britta w polu.</span><span class="sxs-lookup"><span data-stu-id="b3589-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="b3589-191">Pole obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="b3589-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="b3589-192">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3589-192">There is no action item for you in this section.</span></span> <span data-ttu-id="b3589-193">Jeśli użytkownik nie istnieje w polu, nowy jest tworzony podczas próby tooaccess pole.</span><span class="sxs-lookup"><span data-stu-id="b3589-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3589-194">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3589-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3589-195">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBox.</span><span class="sxs-lookup"><span data-stu-id="b3589-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b3589-197">**tooassign tooBox Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b3589-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3589-198">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3589-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b3589-200">Z listy aplikacji hello wybierz **pole**.</span><span class="sxs-lookup"><span data-stu-id="b3589-200">In hello applications list, select **Box**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="b3589-202">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b3589-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b3589-204">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3589-204">Click **Add** button.</span></span> <span data-ttu-id="b3589-205">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3589-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b3589-207">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b3589-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3589-208">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3589-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3589-209">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3589-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3589-210">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3589-210">Testing single sign-on</span></span>

<span data-ttu-id="b3589-211">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3589-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3589-212">Po kliknięciu kafelka pole hello w hello Panel dostępu, należy pobrać logowania strony tooget zalogowane tooyour okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b3589-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3589-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b3589-213">Additional resources</span></span>

* [<span data-ttu-id="b3589-214">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3589-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3589-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3589-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b3589-216">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="b3589-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

