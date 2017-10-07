---
title: 'Samouczek: Integracji Azure Active Directory z pomocy Scout | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Scout pomocy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="30533-103">Samouczek: Integracji Azure Active Directory z Scout pomocy</span><span class="sxs-lookup"><span data-stu-id="30533-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="30533-104">Z tego samouczka dowiesz się, jak toointegrate pomóc Scout w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30533-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30533-105">Możesz uzyskać hello następujące korzyści z integracji z usługą Azure AD Scout pomocy:</span><span class="sxs-lookup"><span data-stu-id="30533-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="30533-106">W usłudze Azure AD można kontrolować, kto ma dostęp do tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="30533-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="30533-107">W Twojej tooHelp użytkowników Scout może automatycznie podpisywać za pomocą rejestracji jednokrotnej i konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30533-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="30533-108">Możesz zarządzać kont w jednej, centralnej lokalizacji, hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="30533-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="30533-109">toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30533-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30533-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="30533-110">Prerequisites</span></span>

<span data-ttu-id="30533-111">tooset się integracji usługi Azure AD z Scout pomocy, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="30533-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="30533-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="30533-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30533-113">Subskrypcja Scout pomocy, z logowanie jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="30533-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="30533-114">W przypadku testowania czynności hello w tym samouczku, zaleca się nie przetestować ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="30533-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="30533-115">Zalecenia dotyczące testowania czynności hello w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="30533-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="30533-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="30533-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="30533-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [Pobierz bezpłatną wersję próbną miesięcznego](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30533-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30533-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="30533-118">Scenario description</span></span>
<span data-ttu-id="30533-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="30533-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="30533-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="30533-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30533-121">Dodaj Scout pomocy z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="30533-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="30533-122">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="30533-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="30533-123">Dodawanie pomocy Scout z galerii hello</span><span class="sxs-lookup"><span data-stu-id="30533-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="30533-124">tooset się hello integracji Pomocy Scout z usługą Azure AD w galerii hello Dodaj pomocy Scout tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="30533-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30533-125">tooadd pomocy Scout z galerii hello:</span><span class="sxs-lookup"><span data-stu-id="30533-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="30533-126">W hello [portalu Azure](https://portal.azure.com), w menu po lewej stronie Witaj, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30533-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="30533-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="30533-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Strona aplikacji Hello Enterprise][2]
    
3. <span data-ttu-id="30533-130">tooadd nowej aplikacji, wybierz **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="30533-130">tooadd a new application, select **New application**.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="30533-132">W polu wyszukiwania hello wpisz **pomocy Scout**.</span><span class="sxs-lookup"><span data-stu-id="30533-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="30533-133">W wynikach wyszukiwania hello, wybierz **pomocy Scout**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="30533-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Pomoc Scout hello listy wyników](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="30533-135">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="30533-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="30533-136">W tej sekcji możesz zdefiniować i test usługi Azure AD rejestracji jednokrotnej z Scout pomoc w oparciu o nazwie użytkownika testowego *Simona Britta*.</span><span class="sxs-lookup"><span data-stu-id="30533-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="30533-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello Azure AD odpowiednikiem użytkownika w Scout pomocy.</span><span class="sxs-lookup"><span data-stu-id="30533-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="30533-138">Należy ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Scout pomocy.</span><span class="sxs-lookup"><span data-stu-id="30533-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="30533-139">Witaj tooestablish łączy relacji w pomocy Scout dla **Username**, przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30533-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="30533-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pomocy Scout pełną hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="30533-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="30533-141">[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="30533-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="30533-142">Konfiguruje toouse użytkownika tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="30533-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="30533-143">[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="30533-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="30533-144">Testy usługi Azure AD rejestracji jednokrotnej z użytkownikiem hello Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="30533-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="30533-145">[Tworzenie użytkownika testowego pomocy Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="30533-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="30533-146">Tworzy odpowiednikiem Simona Britta Scout pomocy, który jest połączony toohello reprezentacja hello użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30533-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="30533-147">[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="30533-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="30533-148">Konfiguruje toouse Simona Britta usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="30533-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30533-149">[Test rejestracji jednokrotnej](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="30533-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="30533-150">Sprawdza, czy konfiguracja tego hello działa.</span><span class="sxs-lookup"><span data-stu-id="30533-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="30533-151">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="30533-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="30533-152">W tej sekcji można skonfigurować usługi Azure AD rejestracji jednokrotnej w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="30533-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="30533-153">Następnie skonfigurowaniu rejestracji jednokrotnej w aplikacji Scout pomocy.</span><span class="sxs-lookup"><span data-stu-id="30533-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="30533-154">tooset się usługi Azure AD rejestracji jednokrotnej z Scout pomocy:</span><span class="sxs-lookup"><span data-stu-id="30533-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="30533-155">W portalu Azure na powitania hello **pomocy Scout** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="30533-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Konfigurowanie łącza rejestracji jednokrotnej][4]

2. <span data-ttu-id="30533-157">Na powitania **logowanie jednokrotne** strony, dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="30533-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="30533-159">W obszarze **pomocy domeny Scout i adres URL**, jeśli chcesz tooset się hello aplikację w trybie inicjowanych przez dostawców tożsamości, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="30533-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="30533-160">W hello **identyfikator** wprowadź adres URL, który ma hello następującego wzorca:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="30533-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="30533-161">W hello **adres URL odpowiedzi** wprowadź adres URL, który ma hello następującego wzorca:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="30533-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Adresy URL i domeny Scout pojedynczego logowania jednokrotnego informacje pomocy](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="30533-163">Tooset się hello aplikację w trybie zainicjował SP, zaznacz hello **Pokaż zaawansowane ustawienia adresu URL** pole wyboru, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="30533-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="30533-164">W hello **Zaloguj się na adres URL** wprowadź adres URL, który ma hello następującego formatu:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="30533-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Adresy URL i domeny Scout pojedynczego logowania jednokrotnego informacje pomocy](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="30533-166">wartości Hello w tych adresów URL dotyczą tylko pokaz.</span><span class="sxs-lookup"><span data-stu-id="30533-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="30533-167">Zaktualizuj wartości hello hello rzeczywisty identyfikator URL i adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="30533-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="30533-168">Skontaktuj się z tych wartości, tooget [Scout pomoc techniczną](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="30533-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="30533-169">W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**, a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="30533-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="30533-171">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="30533-171">Select **Save**.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="30533-173">tooset się jednym logowania po stronie pomocy Scout hello, Wyślij toohello pliku XML metadanych hello pobrane [Scout pomoc techniczną](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="30533-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="30533-174">zespołem pomocy technicznej pomocy Scout Hello dotyczy to ustawienie, aby hello SAML logowania jednokrotnego połączenie jest prawidłowo po obu stronach.</span><span class="sxs-lookup"><span data-stu-id="30533-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="30533-175">Możesz przeczytać zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="30533-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="30533-176">Po dodaniu aplikacji hello wybierając **usługi Active Directory** > **aplikacje dla przedsiębiorstw**, wybierz pozycję hello **rejestracji jednokrotnej** kartę. Dostęp można uzyskać dokumentację hello osadzone w hello **konfiguracji** sekcji u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="30533-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="30533-177">Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="30533-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="30533-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="30533-178">Create an Azure AD test user</span></span>

<span data-ttu-id="30533-179">W tej sekcji w hello portalu Azure utworzysz użytkownika testu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="30533-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="30533-181">toocreate użytkownika testowego w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="30533-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="30533-182">W portalu Azure, w menu po lewej stronie powitania hello wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30533-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="30533-184">toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="30533-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Wybierz użytkowników i grup, a następnie wybierz opcję Wszyscy użytkownicy](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="30533-186">Witaj tooopen **użytkownika** okno dialogowe u góry hello hello **wszyscy użytkownicy** wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="30533-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="30533-188">W hello **użytkownika** okno dialogowe, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="30533-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="30533-189">W hello **nazwa** wprowadź **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30533-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="30533-190">W hello **nazwy użytkownika** wprowadź adres e-mail użytkownika Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="30533-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="30533-191">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="30533-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="30533-192">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="30533-192">Select **Create**.</span></span>

        ![okno dialogowe Hello użytkownika](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="30533-194">Tworzenie użytkownika testowego Scout pomocy</span><span class="sxs-lookup"><span data-stu-id="30533-194">Create a Help Scout test user</span></span>

<span data-ttu-id="30533-195">Witaj w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Scout pomocy.</span><span class="sxs-lookup"><span data-stu-id="30533-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="30533-196">Pomoc Scout obsługuje just in time (JIT) inicjowania obsługi, które jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="30533-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="30533-197">W tej sekcji nie ma żadnych toocomplete akcji lub zadań.</span><span class="sxs-lookup"><span data-stu-id="30533-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="30533-198">Jeśli użytkownik nie istnieje w pomocy Scout, nowy jest tworzony podczas próby tooaccess Scout pomocy.</span><span class="sxs-lookup"><span data-stu-id="30533-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="30533-199">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="30533-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="30533-200">W tej sekcji możesz umożliwia użytkownikowi hello Simona Britta toouse usługi Azure AD rejestracji jednokrotnej, przyznając hello użytkownika konta dostępu tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="30533-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="30533-202">tooassign tooHelp Simona Britta Scout:</span><span class="sxs-lookup"><span data-stu-id="30533-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="30533-203">W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu.</span><span class="sxs-lookup"><span data-stu-id="30533-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="30533-204">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="30533-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="30533-206">Z listy aplikacji hello wybierz **pomocy Scout**.</span><span class="sxs-lookup"><span data-stu-id="30533-206">In hello applications list, select **Help Scout**.</span></span>

    ![łącza pomocy Scout Hello na liście aplikacji hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="30533-208">W menu po lewej stronie powitania wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="30533-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hello użytkowników i grup łącza][202]

4. <span data-ttu-id="30533-210">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="30533-210">Select **Add**.</span></span> <span data-ttu-id="30533-211">Następnie na powitania **Dodaj przydziału** wybierz pozycję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="30533-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="30533-213">Na powitania **użytkowników i grup** strony w hello listę użytkowników, wybierz opcję **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="30533-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="30533-214">Na powitania **użytkowników i grup** wybierz pozycję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="30533-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="30533-215">Na powitania **Dodaj przydziału** wybierz pozycję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="30533-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="30533-216">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="30533-216">Test single sign-on</span></span>

<span data-ttu-id="30533-217">W tej sekcji można przetestować przy użyciu panelu dostępu hello konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="30533-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="30533-218">Po wybraniu kafelka pomocy Scout hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour pomocy Scout aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30533-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="30533-219">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [panelu dostępu toohello wprowadzenie](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="30533-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="30533-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="30533-220">Additional resources</span></span>

* [<span data-ttu-id="30533-221">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30533-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30533-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="30533-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

