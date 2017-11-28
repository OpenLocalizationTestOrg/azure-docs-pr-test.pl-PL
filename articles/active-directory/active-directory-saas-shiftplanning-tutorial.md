---
title: "Samouczek: Integracji Azure Active Directory z ludzkości | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ludzkości."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="effd1-103">Samouczek: Integracji Azure Active Directory z ludzkości</span><span class="sxs-lookup"><span data-stu-id="effd1-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="effd1-104">Z tego samouczka, dowiesz się, jak toointegrate ludzkości w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="effd1-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="effd1-105">Integracja z usługą Azure AD ludzkości zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="effd1-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="effd1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHumanity</span><span class="sxs-lookup"><span data-stu-id="effd1-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="effd1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHumanity (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="effd1-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="effd1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="effd1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="effd1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="effd1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="effd1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="effd1-110">Prerequisites</span></span>

<span data-ttu-id="effd1-111">tooconfigure integracji z usługą Azure AD z ludzkości należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="effd1-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="effd1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="effd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="effd1-113">Ludzkości jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="effd1-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="effd1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="effd1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="effd1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="effd1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="effd1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="effd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="effd1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="effd1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="effd1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="effd1-118">Scenario description</span></span>
<span data-ttu-id="effd1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="effd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="effd1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="effd1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="effd1-121">Dodawanie ludzkości z galerii hello</span><span class="sxs-lookup"><span data-stu-id="effd1-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="effd1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="effd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="effd1-123">Dodawanie ludzkości z galerii hello</span><span class="sxs-lookup"><span data-stu-id="effd1-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="effd1-124">integracji hello tooconfigure ludzkości do usługi Azure AD, należy tooadd ludzkości z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="effd1-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="effd1-125">**tooadd ludzkości z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="effd1-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="effd1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="effd1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="effd1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="effd1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="effd1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="effd1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="effd1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="effd1-133">W polu wyszukiwania hello wpisz **ludzkości**.</span><span class="sxs-lookup"><span data-stu-id="effd1-133">In hello search box, type **Humanity**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="effd1-135">W panelu wyników hello zaznacz **ludzkości**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="effd1-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="effd1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="effd1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="effd1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ludzkości oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="effd1-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="effd1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ludzkości jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="effd1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="effd1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ludzkości musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="effd1-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="effd1-141">W ludzkości, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="effd1-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="effd1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ludzkości, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="effd1-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="effd1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="effd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="effd1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="effd1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="effd1-145">**[Tworzenie użytkownika testowego ludzkości](#creating-a-humanity-test-user)**  -toohave odpowiednikiem Simona Britta w ludzkości, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="effd1-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="effd1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="effd1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="effd1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="effd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="effd1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="effd1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="effd1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ludzkości.</span><span class="sxs-lookup"><span data-stu-id="effd1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="effd1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ludzkości, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="effd1-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="effd1-151">W portalu Azure na powitania hello **ludzkości** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="effd1-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="effd1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="effd1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="effd1-155">Na powitania **ludzkości domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="effd1-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="effd1-157">a.</span><span class="sxs-lookup"><span data-stu-id="effd1-157">a.</span></span> <span data-ttu-id="effd1-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="effd1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="effd1-159">b.</span><span class="sxs-lookup"><span data-stu-id="effd1-159">b.</span></span> <span data-ttu-id="effd1-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="effd1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="effd1-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="effd1-161">These values are not real.</span></span> <span data-ttu-id="effd1-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="effd1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="effd1-163">Skontaktuj się z [zespołem pomocy technicznej klienta ludzkości](https://www.humanity.com/support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="effd1-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="effd1-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="effd1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="effd1-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="effd1-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="effd1-168">Na powitania **konfiguracji ludzkości** kliknij **skonfigurować ludzkości** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="effd1-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="effd1-169">Witaj kopii **SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="effd1-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="effd1-171">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **ludzkości** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="effd1-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="effd1-172">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="effd1-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="effd1-173">![Administrator](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="effd1-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="effd1-174">W obszarze **integracji**, kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="effd1-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="effd1-175">![Logowanie jednokrotne](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="effd1-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="effd1-176">W hello **rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="effd1-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="effd1-177">![Logowanie jednokrotne](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="effd1-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="effd1-178">a.</span><span class="sxs-lookup"><span data-stu-id="effd1-178">a.</span></span> <span data-ttu-id="effd1-179">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="effd1-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="effd1-180">b.</span><span class="sxs-lookup"><span data-stu-id="effd1-180">b.</span></span> <span data-ttu-id="effd1-181">Wybierz **Zezwalaj na hasło logowania**.</span><span class="sxs-lookup"><span data-stu-id="effd1-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="effd1-182">c.</span><span class="sxs-lookup"><span data-stu-id="effd1-182">c.</span></span> <span data-ttu-id="effd1-183">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartości do hello **adres URL wystawcy SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="effd1-184">d.</span><span class="sxs-lookup"><span data-stu-id="effd1-184">d.</span></span> <span data-ttu-id="effd1-185">Wklej hello **Sign-Out URL** wartości do hello **zdalnego adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="effd1-186">e.</span><span class="sxs-lookup"><span data-stu-id="effd1-186">e.</span></span> <span data-ttu-id="effd1-187">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="effd1-188">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="effd1-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="effd1-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="effd1-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="effd1-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="effd1-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="effd1-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="effd1-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="effd1-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="effd1-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="effd1-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="effd1-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="effd1-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="effd1-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="effd1-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="effd1-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="effd1-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="effd1-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="effd1-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="effd1-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="effd1-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="effd1-204">a.</span><span class="sxs-lookup"><span data-stu-id="effd1-204">a.</span></span> <span data-ttu-id="effd1-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="effd1-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="effd1-206">b.</span><span class="sxs-lookup"><span data-stu-id="effd1-206">b.</span></span> <span data-ttu-id="effd1-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="effd1-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="effd1-208">c.</span><span class="sxs-lookup"><span data-stu-id="effd1-208">c.</span></span> <span data-ttu-id="effd1-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="effd1-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="effd1-210">d.</span><span class="sxs-lookup"><span data-stu-id="effd1-210">d.</span></span> <span data-ttu-id="effd1-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="effd1-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="effd1-212">Tworzenie użytkownika testowego ludzkości</span><span class="sxs-lookup"><span data-stu-id="effd1-212">Creating a Humanity test user</span></span>

<span data-ttu-id="effd1-213">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooHumanity muszą mieć przydzielone do ludzkości.</span><span class="sxs-lookup"><span data-stu-id="effd1-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="effd1-214">W przypadku hello ludzkości Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="effd1-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="effd1-215">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="effd1-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="effd1-216">Zaloguj się za tooyour **ludzkości** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="effd1-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="effd1-217">Kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="effd1-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="effd1-218">![Administrator](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="effd1-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="effd1-219">Kliknij przycisk **personelu**.</span><span class="sxs-lookup"><span data-stu-id="effd1-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="effd1-220">![Personel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personelu")</span><span class="sxs-lookup"><span data-stu-id="effd1-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="effd1-221">W obszarze **akcje**, kliknij przycisk **dodać pracowników**.</span><span class="sxs-lookup"><span data-stu-id="effd1-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="effd1-222">![Dodaj pracowników](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "dodać pracowników")</span><span class="sxs-lookup"><span data-stu-id="effd1-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="effd1-223">W hello **dodać pracowników** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="effd1-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="effd1-224">![Zapisz pracowników](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "zapisać pracowników")</span><span class="sxs-lookup"><span data-stu-id="effd1-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="effd1-225">a.</span><span class="sxs-lookup"><span data-stu-id="effd1-225">a.</span></span> <span data-ttu-id="effd1-226">Typ hello **imię**, **nazwisko**, i **E-mail** z prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="effd1-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="effd1-227">b.</span><span class="sxs-lookup"><span data-stu-id="effd1-227">b.</span></span> <span data-ttu-id="effd1-228">Kliknij przycisk **zapisać pracowników**.</span><span class="sxs-lookup"><span data-stu-id="effd1-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="effd1-229">Możesz użyć innych ludzkości użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision ludzkości kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="effd1-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="effd1-230">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="effd1-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="effd1-231">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHumanity.</span><span class="sxs-lookup"><span data-stu-id="effd1-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="effd1-233">**tooassign tooHumanity Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="effd1-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="effd1-234">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="effd1-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="effd1-236">Z listy aplikacji hello wybierz **ludzkości**.</span><span class="sxs-lookup"><span data-stu-id="effd1-236">In hello applications list, select **Humanity**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="effd1-238">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="effd1-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="effd1-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="effd1-240">Click **Add** button.</span></span> <span data-ttu-id="effd1-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="effd1-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="effd1-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="effd1-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="effd1-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="effd1-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="effd1-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="effd1-246">Testing single sign-on</span></span>

<span data-ttu-id="effd1-247">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="effd1-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="effd1-248">Po kliknięciu kafelka ludzkości hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ludzkości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="effd1-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="effd1-249">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="effd1-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="effd1-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="effd1-250">Additional resources</span></span>

* [<span data-ttu-id="effd1-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="effd1-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="effd1-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="effd1-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

