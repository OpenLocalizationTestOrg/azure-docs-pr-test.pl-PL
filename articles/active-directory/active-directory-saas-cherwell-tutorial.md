---
title: 'Samouczek: Integracji Azure Active Directory z Cherwell | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Cherwell."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: a67b3d346a6f7b43a7e87fb4d9c533f9363f2e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="8b332-103">Samouczek: Integracji Azure Active Directory z Cherwell</span><span class="sxs-lookup"><span data-stu-id="8b332-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="8b332-104">Z tego samouczka, dowiesz się, jak toointegrate Cherwell w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b332-104">In this tutorial, you learn how toointegrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b332-105">Integracja z usługą Azure AD Cherwell zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8b332-105">Integrating Cherwell with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b332-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCherwell</span><span class="sxs-lookup"><span data-stu-id="8b332-106">You can control in Azure AD who has access tooCherwell</span></span>
- <span data-ttu-id="8b332-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCherwell (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b332-107">You can enable your users tooautomatically get signed-on tooCherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b332-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8b332-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8b332-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b332-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b332-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b332-110">Prerequisites</span></span>

<span data-ttu-id="8b332-111">tooconfigure integracji z usługą Azure AD z Cherwell należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8b332-111">tooconfigure Azure AD integration with Cherwell, you need hello following items:</span></span>

- <span data-ttu-id="8b332-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b332-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b332-113">Cherwell jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8b332-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b332-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8b332-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b332-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8b332-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b332-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8b332-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b332-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b332-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b332-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8b332-118">Scenario description</span></span>
<span data-ttu-id="8b332-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8b332-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b332-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8b332-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b332-121">Dodawanie Cherwell z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b332-121">Adding Cherwell from hello gallery</span></span>
2. <span data-ttu-id="8b332-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b332-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-hello-gallery"></a><span data-ttu-id="8b332-123">Dodawanie Cherwell z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b332-123">Adding Cherwell from hello gallery</span></span>
<span data-ttu-id="8b332-124">tooconfigure hello integracji Cherwell do usługi Azure AD, należy tooadd Cherwell z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b332-124">tooconfigure hello integration of Cherwell into Azure AD, you need tooadd Cherwell from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b332-125">**tooadd Cherwell z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b332-125">**tooadd Cherwell from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b332-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b332-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8b332-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8b332-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b332-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b332-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8b332-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b332-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8b332-133">W polu wyszukiwania hello wpisz **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="8b332-133">In hello search box, type **Cherwell**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="8b332-135">W panelu wyników hello zaznacz **Cherwell**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8b332-135">In hello results panel, select **Cherwell**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b332-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b332-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b332-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Cherwell na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8b332-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b332-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Cherwell jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b332-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cherwell is tooa user in Azure AD.</span></span> <span data-ttu-id="8b332-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Cherwell musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8b332-140">In other words, a link relationship between an Azure AD user and hello related user in Cherwell needs toobe established.</span></span>

<span data-ttu-id="8b332-141">W Cherwell, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8b332-141">In Cherwell, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b332-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Cherwell, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8b332-142">tooconfigure and test Azure AD single sign-on with Cherwell, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b332-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8b332-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b332-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b332-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b332-145">**[Tworzenie użytkownika testowego Cherwell](#creating-a-cherwell-test-user)**  -toohave odpowiednikiem Simona Britta w Cherwell, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b332-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - toohave a counterpart of Britta Simon in Cherwell that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b332-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b332-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b332-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8b332-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b332-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b332-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b332-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Cherwell.</span><span class="sxs-lookup"><span data-stu-id="8b332-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="8b332-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Cherwell, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b332-150">**tooconfigure Azure AD single sign-on with Cherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b332-151">W portalu Azure na powitania hello **Cherwell** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8b332-151">In hello Azure portal, on hello **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8b332-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b332-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="8b332-155">Na powitania **Cherwell domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8b332-155">On hello **Cherwell Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="8b332-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="8b332-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b332-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8b332-158">This value is not real.</span></span> <span data-ttu-id="8b332-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8b332-159">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="8b332-160">Skontaktuj się z [zespołem pomocy technicznej Cherwell](https://csm.cherwell.com/contact) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="8b332-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) tooget this value.</span></span>
 
4. <span data-ttu-id="8b332-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8b332-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="8b332-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b332-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b332-165">Na powitania **konfiguracji Cherwell** kliknij **skonfigurować Cherwell** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8b332-165">On hello **Cherwell Configuration** section, click **Configure Cherwell** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8b332-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8b332-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="8b332-168">tooconfigure rejestracji jednokrotnej w **Cherwell** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **SAML pojedynczy znak na adres URL usługi**, i  **Identyfikator jednostki SAML** za[zespołem pomocy technicznej Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="8b332-168">tooconfigure single sign-on on **Cherwell** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="8b332-169">Z zespołem pomocy technicznej Cherwell ma toodo hello rzeczywista konfiguracja logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="8b332-169">Your Cherwell support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="8b332-170">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8b332-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="8b332-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8b332-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b332-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8b332-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b332-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b332-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b332-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b332-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b332-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8b332-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8b332-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b332-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b332-178">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b332-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b332-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8b332-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b332-182">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b332-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b332-184">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b332-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b332-186">a.</span><span class="sxs-lookup"><span data-stu-id="8b332-186">a.</span></span> <span data-ttu-id="8b332-187">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b332-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b332-188">b.</span><span class="sxs-lookup"><span data-stu-id="8b332-188">b.</span></span> <span data-ttu-id="8b332-189">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b332-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b332-190">c.</span><span class="sxs-lookup"><span data-stu-id="8b332-190">c.</span></span> <span data-ttu-id="8b332-191">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8b332-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8b332-192">d.</span><span class="sxs-lookup"><span data-stu-id="8b332-192">d.</span></span> <span data-ttu-id="8b332-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8b332-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="8b332-194">Tworzenie użytkownika testowego Cherwell</span><span class="sxs-lookup"><span data-stu-id="8b332-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="8b332-195">toolog użytkowników tooenable usługi Azure AD w tooCherwell, muszą mieć przydzielone do Cherwell.</span><span class="sxs-lookup"><span data-stu-id="8b332-195">tooenable Azure AD users toolog in tooCherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="8b332-196">W przypadku hello Cherwell, hello konta użytkowników muszą toobe utworzone przez użytkownika [zespołem pomocy technicznej Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="8b332-196">In hello case of Cherwell, hello user accounts need toobe created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="8b332-197">Możesz użyć innych Cherwell użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Cherwell usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8b332-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b332-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b332-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8b332-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCherwell.</span><span class="sxs-lookup"><span data-stu-id="8b332-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCherwell.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8b332-201">**tooassign tooCherwell Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8b332-201">**tooassign Britta Simon tooCherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b332-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b332-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8b332-204">Z listy aplikacji hello wybierz **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="8b332-204">In hello applications list, select **Cherwell**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="8b332-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8b332-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8b332-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b332-208">Click **Add** button.</span></span> <span data-ttu-id="8b332-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b332-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8b332-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8b332-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b332-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b332-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b332-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b332-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b332-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b332-214">Testing single sign-on</span></span>

<span data-ttu-id="8b332-215">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8b332-215">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8b332-216">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b332-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b332-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8b332-217">Additional resources</span></span>

* [<span data-ttu-id="8b332-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b332-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b332-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b332-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

