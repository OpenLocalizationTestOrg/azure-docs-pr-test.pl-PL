---
title: 'Samouczek: Integracji Azure Active Directory z 360 Online | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i 360 Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 413e4e2c41336f99e1999857c788c5dac15be4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="a7b08-103">Samouczek: Integracji Azure Active Directory z 360 Online</span><span class="sxs-lookup"><span data-stu-id="a7b08-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="a7b08-104">Z tego samouczka, dowiesz się, jak toointegrate 360 w trybie Online w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7b08-104">In this tutorial, you learn how toointegrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7b08-105">Integrowanie 360 Online z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a7b08-105">Integrating 360 Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7b08-106">Można kontrolować w usłudze Azure AD, kto ma dostęp too360 Online</span><span class="sxs-lookup"><span data-stu-id="a7b08-106">You can control in Azure AD who has access too360 Online</span></span>
- <span data-ttu-id="a7b08-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane too360 Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7b08-107">You can enable your users tooautomatically get signed-on too360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7b08-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a7b08-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7b08-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7b08-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7b08-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a7b08-110">Prerequisites</span></span>

<span data-ttu-id="a7b08-111">tooconfigure integracji usługi Azure AD z 360 Online należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a7b08-111">tooconfigure Azure AD integration with 360 Online, you need hello following items:</span></span>

- <span data-ttu-id="a7b08-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7b08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7b08-113">360 Online jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a7b08-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7b08-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7b08-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a7b08-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7b08-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a7b08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7b08-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7b08-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7b08-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a7b08-118">Scenario description</span></span>
<span data-ttu-id="a7b08-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a7b08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7b08-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a7b08-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7b08-121">Dodawanie 360 Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a7b08-121">Adding 360 Online from hello gallery</span></span>
2. <span data-ttu-id="a7b08-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a7b08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-hello-gallery"></a><span data-ttu-id="a7b08-123">Dodawanie 360 Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a7b08-123">Adding 360 Online from hello gallery</span></span>
<span data-ttu-id="a7b08-124">tooconfigure hello integracji 360 Online z usługą Azure AD, należy tooadd 360 Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7b08-124">tooconfigure hello integration of 360 Online into Azure AD, you need tooadd 360 Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7b08-125">**tooadd 360 Online z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a7b08-125">**tooadd 360 Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7b08-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a7b08-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a7b08-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7b08-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a7b08-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a7b08-133">W polu wyszukiwania hello wpisz **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-133">In hello search box, type **360 Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="a7b08-135">W panelu wyników hello, wybierz **360 Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7b08-135">In hello results panel, select **360 Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7b08-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a7b08-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7b08-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 360 Online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a7b08-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7b08-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w 360 Online jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7b08-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 360 Online is tooa user in Azure AD.</span></span> <span data-ttu-id="a7b08-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w 360 Online musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a7b08-140">In other words, a link relationship between an Azure AD user and hello related user in 360 Online needs toobe established.</span></span>

<span data-ttu-id="a7b08-141">W trybie Online 360, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="a7b08-141">In 360 Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a7b08-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z 360 Online, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a7b08-142">tooconfigure and test Azure AD single sign-on with 360 Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7b08-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a7b08-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7b08-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a7b08-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7b08-145">**[Tworzenie użytkownika testowego Online 360](#creating-a-360-online-test-user)**  -toohave odpowiednikiem Simona Britta w 360 Online, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a7b08-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - toohave a counterpart of Britta Simon in 360 Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7b08-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a7b08-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7b08-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a7b08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7b08-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a7b08-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7b08-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne 360 aplikacji Online.</span><span class="sxs-lookup"><span data-stu-id="a7b08-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="a7b08-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z 360 Online, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a7b08-150">**tooconfigure Azure AD single sign-on with 360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7b08-151">W portalu Azure na powitania hello **360 Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-151">In hello Azure portal, on hello **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a7b08-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a7b08-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="a7b08-155">Na powitania **360 domeny w trybie Online i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a7b08-155">On hello **360 Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="a7b08-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="a7b08-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7b08-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a7b08-158">hello value is not real.</span></span> <span data-ttu-id="a7b08-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="a7b08-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a7b08-160">Skontaktuj się z [360 zespołem pomocy technicznej Online klienta](mailto:360online@software-innovation.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="a7b08-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="a7b08-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a7b08-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="a7b08-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a7b08-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7b08-165">tooconfigure rejestracji jednokrotnej w **360 Online** strony, należy pobrać hello toosend **XML metadanych** za[360 Online obsługuje zespołu](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="a7b08-165">tooconfigure single sign-on on **360 Online** side, you need toosend hello downloaded **Metadata XML** too[360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a7b08-166">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a7b08-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7b08-167">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a7b08-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7b08-168">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7b08-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7b08-169">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7b08-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7b08-170">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a7b08-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a7b08-172">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a7b08-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7b08-173">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a7b08-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7b08-175">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7b08-177">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7b08-179">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a7b08-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7b08-181">a.</span><span class="sxs-lookup"><span data-stu-id="a7b08-181">a.</span></span> <span data-ttu-id="a7b08-182">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7b08-183">b.</span><span class="sxs-lookup"><span data-stu-id="a7b08-183">b.</span></span> <span data-ttu-id="a7b08-184">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7b08-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7b08-185">c.</span><span class="sxs-lookup"><span data-stu-id="a7b08-185">c.</span></span> <span data-ttu-id="a7b08-186">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7b08-187">d.</span><span class="sxs-lookup"><span data-stu-id="a7b08-187">d.</span></span> <span data-ttu-id="a7b08-188">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="a7b08-189">Tworzenie użytkownika testowego Online 360</span><span class="sxs-lookup"><span data-stu-id="a7b08-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="a7b08-190">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w 360 Online.</span><span class="sxs-lookup"><span data-stu-id="a7b08-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="a7b08-191">należy toocontact [360 Online obsługuje zespołu](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="a7b08-191">you need toocontact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7b08-192">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7b08-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7b08-193">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu too360 w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="a7b08-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too360 Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a7b08-195">**tooassign Simona Britta too360 Online, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a7b08-195">**tooassign Britta Simon too360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7b08-196">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a7b08-198">Z listy aplikacji hello wybierz **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-198">In hello applications list, select **360 Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="a7b08-200">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a7b08-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a7b08-202">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a7b08-202">Click **Add** button.</span></span> <span data-ttu-id="a7b08-203">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a7b08-205">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a7b08-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7b08-206">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7b08-207">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a7b08-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7b08-208">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a7b08-208">Testing single sign-on</span></span>

<span data-ttu-id="a7b08-209">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7b08-209">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7b08-210">Po kliknięciu hello 360 Online kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour 360 aplikacji Online.</span><span class="sxs-lookup"><span data-stu-id="a7b08-210">When you click hello 360 Online tile in hello Access Panel, you should get automatically signed-on tooyour 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7b08-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a7b08-211">Additional resources</span></span>

* [<span data-ttu-id="a7b08-212">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7b08-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7b08-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7b08-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

