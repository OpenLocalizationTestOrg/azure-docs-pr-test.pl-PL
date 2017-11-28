---
title: 'Samouczek: Integracji Azure Active Directory z Jostle | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jostle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 617375d8f9e1cebcdb28450fc8d0ad8af99d7b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="6187a-103">Samouczek: Integracji Azure Active Directory z Jostle</span><span class="sxs-lookup"><span data-stu-id="6187a-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="6187a-104">Z tego samouczka, dowiesz się, jak toointegrate Jostle z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6187a-104">In this tutorial, you learn how toointegrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6187a-105">Integracja z usługą Azure AD Jostle zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6187a-105">Integrating Jostle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6187a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJostle</span><span class="sxs-lookup"><span data-stu-id="6187a-106">You can control in Azure AD who has access tooJostle</span></span>
- <span data-ttu-id="6187a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJostle (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6187a-107">You can enable your users tooautomatically get signed-on tooJostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6187a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6187a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6187a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6187a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6187a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6187a-110">Prerequisites</span></span>

<span data-ttu-id="6187a-111">Integracja tooconfigure usługi Azure AD z Jostle, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6187a-111">tooconfigure Azure AD integration with Jostle, you need hello following items:</span></span>

- <span data-ttu-id="6187a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6187a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6187a-113">Jostle jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6187a-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6187a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6187a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6187a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6187a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6187a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6187a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6187a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6187a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6187a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6187a-118">Scenario description</span></span>
<span data-ttu-id="6187a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6187a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6187a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6187a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6187a-121">Dodawanie Jostle z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6187a-121">Adding Jostle from hello gallery</span></span>
2. <span data-ttu-id="6187a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6187a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-hello-gallery"></a><span data-ttu-id="6187a-123">Dodawanie Jostle z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6187a-123">Adding Jostle from hello gallery</span></span>
<span data-ttu-id="6187a-124">tooconfigure hello integracji Jostle do usługi Azure AD, należy tooadd Jostle z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6187a-124">tooconfigure hello integration of Jostle into Azure AD, you need tooadd Jostle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6187a-125">**tooadd Jostle z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6187a-125">**tooadd Jostle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6187a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6187a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6187a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6187a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6187a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6187a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6187a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6187a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6187a-133">W polu wyszukiwania hello wpisz **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="6187a-133">In hello search box, type **Jostle**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="6187a-135">W panelu wyników hello zaznacz **Jostle**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6187a-135">In hello results panel, select **Jostle**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6187a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6187a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6187a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jostle na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6187a-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6187a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Jostle jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6187a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jostle is tooa user in Azure AD.</span></span> <span data-ttu-id="6187a-140">Innymi słowy link relację między użytkownika usługi Azure AD i hello użytkownikowi w toobe potrzeb Jostle ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6187a-140">In other words, a link relationship between an Azure AD user and hello related user in Jostle needs toobe established.</span></span>

<span data-ttu-id="6187a-141">W Jostle, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6187a-141">In Jostle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6187a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Jostle, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6187a-142">tooconfigure and test Azure AD single sign-on with Jostle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6187a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6187a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6187a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6187a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6187a-145">**[Tworzenie użytkownika testowego Jostle](#creating-a-jostle-test-user)**  -toohave odpowiednikiem Simona Britta w Jostle, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6187a-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - toohave a counterpart of Britta Simon in Jostle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6187a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6187a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6187a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6187a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6187a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6187a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6187a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Jostle.</span><span class="sxs-lookup"><span data-stu-id="6187a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="6187a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Jostle, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6187a-150">**tooconfigure Azure AD single sign-on with Jostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6187a-151">W portalu Azure na powitania hello **Jostle** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6187a-151">In hello Azure portal, on hello **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6187a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6187a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="6187a-155">Na powitania **Jostle domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6187a-155">On hello **Jostle Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="6187a-157">a.</span><span class="sxs-lookup"><span data-stu-id="6187a-157">a.</span></span> <span data-ttu-id="6187a-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="6187a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="6187a-159">b.</span><span class="sxs-lookup"><span data-stu-id="6187a-159">b.</span></span> <span data-ttu-id="6187a-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="6187a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6187a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6187a-161">These values are not real.</span></span> <span data-ttu-id="6187a-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="6187a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6187a-163">Skontaktuj się z [zespołem pomocy technicznej Jostle](mailto:support@jostle.me) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6187a-163">Contact [Jostle support team](mailto:support@jostle.me) tooget these values.</span></span> 
 


4. <span data-ttu-id="6187a-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6187a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="6187a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6187a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6187a-168">tooconfigure rejestracji jednokrotnej po stronie Jostle, należy toosend hello pobrane XML metadanych zbyt[zespołem pomocy technicznej Jostle](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="6187a-168">tooconfigure single sign-on on Jostle side, you need toosend hello downloaded metadata XML too[Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="6187a-169">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="6187a-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="6187a-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6187a-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6187a-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6187a-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6187a-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6187a-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6187a-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6187a-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="6187a-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6187a-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6187a-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6187a-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6187a-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6187a-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6187a-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6187a-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6187a-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6187a-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6187a-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6187a-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6187a-185">a.</span><span class="sxs-lookup"><span data-stu-id="6187a-185">a.</span></span> <span data-ttu-id="6187a-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6187a-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6187a-187">b.</span><span class="sxs-lookup"><span data-stu-id="6187a-187">b.</span></span> <span data-ttu-id="6187a-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6187a-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6187a-189">c.</span><span class="sxs-lookup"><span data-stu-id="6187a-189">c.</span></span> <span data-ttu-id="6187a-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6187a-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6187a-191">d.</span><span class="sxs-lookup"><span data-stu-id="6187a-191">d.</span></span> <span data-ttu-id="6187a-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6187a-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="6187a-193">Tworzenie użytkownika testowego Jostle</span><span class="sxs-lookup"><span data-stu-id="6187a-193">Creating a Jostle test user</span></span>

<span data-ttu-id="6187a-194">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Jostle.</span><span class="sxs-lookup"><span data-stu-id="6187a-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="6187a-195">Jeśli nie wiadomo jak tooadd Simona Britta w Jostle, skontaktuj się z [zespołem pomocy technicznej Jostle](mailto:support@jostle.me) tooadd hello użytkownika testowego i włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="6187a-195">If you don't know how tooadd Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) tooadd hello test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="6187a-196">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="6187a-196">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6187a-197">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6187a-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6187a-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJostle.</span><span class="sxs-lookup"><span data-stu-id="6187a-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJostle.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6187a-200">**tooassign tooJostle Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6187a-200">**tooassign Britta Simon tooJostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6187a-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6187a-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6187a-203">Z listy aplikacji hello wybierz **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="6187a-203">In hello applications list, select **Jostle**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="6187a-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6187a-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6187a-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6187a-207">Click **Add** button.</span></span> <span data-ttu-id="6187a-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6187a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6187a-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6187a-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6187a-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6187a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6187a-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6187a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6187a-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6187a-213">Testing single sign-on</span></span>

<span data-ttu-id="6187a-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6187a-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6187a-215">Po kliknięciu kafelka Jostle hello w hello Panel dostępu, należy uzyskać automatycznie strony logowania Jostle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6187a-215">When you click hello Jostle tile in hello Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="6187a-216">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6187a-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6187a-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6187a-217">Additional resources</span></span>

* [<span data-ttu-id="6187a-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6187a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6187a-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6187a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

