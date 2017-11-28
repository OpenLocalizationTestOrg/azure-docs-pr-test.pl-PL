---
title: 'Samouczek: Integracji Azure Active Directory z Sciforma | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Sciforma."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: fca6237196061355e38d431e958964a45246f965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="e47bf-103">Samouczek: Integracji Azure Active Directory z Sciforma</span><span class="sxs-lookup"><span data-stu-id="e47bf-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="e47bf-104">Z tego samouczka, dowiesz się, jak toointegrate Sciforma w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e47bf-104">In this tutorial, you learn how toointegrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e47bf-105">Integracja z usługą Azure AD Sciforma zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e47bf-105">Integrating Sciforma with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e47bf-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSciforma</span><span class="sxs-lookup"><span data-stu-id="e47bf-106">You can control in Azure AD who has access tooSciforma</span></span>
- <span data-ttu-id="e47bf-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSciforma (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e47bf-107">You can enable your users tooautomatically get signed-on tooSciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e47bf-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e47bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e47bf-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e47bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e47bf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e47bf-110">Prerequisites</span></span>

<span data-ttu-id="e47bf-111">tooconfigure integracji z usługą Azure AD z Sciforma należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e47bf-111">tooconfigure Azure AD integration with Sciforma, you need hello following items:</span></span>

- <span data-ttu-id="e47bf-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e47bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e47bf-113">Sciforma jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e47bf-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e47bf-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e47bf-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e47bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e47bf-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e47bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e47bf-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e47bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e47bf-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e47bf-118">Scenario description</span></span>
<span data-ttu-id="e47bf-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e47bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e47bf-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e47bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e47bf-121">Dodawanie Sciforma z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e47bf-121">Adding Sciforma from hello gallery</span></span>
2. <span data-ttu-id="e47bf-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e47bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-hello-gallery"></a><span data-ttu-id="e47bf-123">Dodawanie Sciforma z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e47bf-123">Adding Sciforma from hello gallery</span></span>
<span data-ttu-id="e47bf-124">tooconfigure hello integracji Sciforma do usługi Azure AD, należy tooadd Sciforma z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e47bf-124">tooconfigure hello integration of Sciforma into Azure AD, you need tooadd Sciforma from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e47bf-125">**tooadd Sciforma z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e47bf-125">**tooadd Sciforma from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e47bf-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e47bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e47bf-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e47bf-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e47bf-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e47bf-133">W polu wyszukiwania hello wpisz **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-133">In hello search box, type **Sciforma**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="e47bf-135">W panelu wyników hello zaznacz **Sciforma**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e47bf-135">In hello results panel, select **Sciforma**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e47bf-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e47bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e47bf-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sciforma na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e47bf-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e47bf-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Sciforma jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e47bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sciforma is tooa user in Azure AD.</span></span> <span data-ttu-id="e47bf-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Sciforma musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e47bf-140">In other words, a link relationship between an Azure AD user and hello related user in Sciforma needs toobe established.</span></span>

<span data-ttu-id="e47bf-141">W Sciforma, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e47bf-141">In Sciforma, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e47bf-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Sciforma, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e47bf-142">tooconfigure and test Azure AD single sign-on with Sciforma, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e47bf-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e47bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e47bf-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e47bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e47bf-145">**[Tworzenie użytkownika testowego Sciforma](#creating-a-sciforma-test-user)**  -toohave odpowiednikiem Simona Britta w Sciforma, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e47bf-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - toohave a counterpart of Britta Simon in Sciforma that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e47bf-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e47bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e47bf-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e47bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e47bf-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e47bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e47bf-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Sciforma.</span><span class="sxs-lookup"><span data-stu-id="e47bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="e47bf-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Sciforma, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e47bf-150">**tooconfigure Azure AD single sign-on with Sciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="e47bf-151">W portalu Azure na powitania hello **Sciforma** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-151">In hello Azure portal, on hello **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e47bf-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e47bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="e47bf-155">Na powitania **Sciforma domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e47bf-155">On hello **Sciforma Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="e47bf-157">a.</span><span class="sxs-lookup"><span data-stu-id="e47bf-157">a.</span></span> <span data-ttu-id="e47bf-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="e47bf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="e47bf-159">b.</span><span class="sxs-lookup"><span data-stu-id="e47bf-159">b.</span></span> <span data-ttu-id="e47bf-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="e47bf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e47bf-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e47bf-161">These values are not real.</span></span> <span data-ttu-id="e47bf-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e47bf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e47bf-163">Skontaktuj się z [zespołem pomocy technicznej klienta Sciforma](http://www.sciforma.com/company/contact_us) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e47bf-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) tooget these values.</span></span> 
 


4. <span data-ttu-id="e47bf-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e47bf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="e47bf-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e47bf-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e47bf-168">tooconfigure rejestracji jednokrotnej w **Sciforma** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Sciforma](http://www.sciforma.com/company/contact_us).</span><span class="sxs-lookup"><span data-stu-id="e47bf-168">tooconfigure single sign-on on **Sciforma** side, you need toosend hello downloaded **Metadata XML** too[Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="e47bf-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e47bf-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e47bf-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e47bf-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e47bf-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e47bf-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e47bf-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e47bf-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e47bf-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e47bf-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e47bf-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e47bf-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e47bf-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e47bf-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e47bf-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e47bf-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e47bf-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e47bf-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e47bf-184">a.</span><span class="sxs-lookup"><span data-stu-id="e47bf-184">a.</span></span> <span data-ttu-id="e47bf-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e47bf-186">b.</span><span class="sxs-lookup"><span data-stu-id="e47bf-186">b.</span></span> <span data-ttu-id="e47bf-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e47bf-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e47bf-188">c.</span><span class="sxs-lookup"><span data-stu-id="e47bf-188">c.</span></span> <span data-ttu-id="e47bf-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e47bf-190">d.</span><span class="sxs-lookup"><span data-stu-id="e47bf-190">d.</span></span> <span data-ttu-id="e47bf-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="e47bf-192">Tworzenie użytkownika testowego Sciforma</span><span class="sxs-lookup"><span data-stu-id="e47bf-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="e47bf-193">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="e47bf-193">There is no action item for you tooconfigure user provisioning tooSciforma.</span></span> <span data-ttu-id="e47bf-194">Gdy przypisany użytkownik podejmie próbę toolog w tooSciforma za pomocą panelu dostępu hello, Sciforma sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e47bf-194">When an assigned user tries toolog in tooSciforma using hello access panel, Sciforma checks whether hello user exists.</span></span>  

* <span data-ttu-id="e47bf-195">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Sciforma.</span><span class="sxs-lookup"><span data-stu-id="e47bf-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e47bf-196">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e47bf-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e47bf-197">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="e47bf-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSciforma.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e47bf-199">**tooassign tooSciforma Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e47bf-199">**tooassign Britta Simon tooSciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="e47bf-200">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e47bf-202">Z listy aplikacji hello wybierz **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-202">In hello applications list, select **Sciforma**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="e47bf-204">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e47bf-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e47bf-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e47bf-206">Click **Add** button.</span></span> <span data-ttu-id="e47bf-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e47bf-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e47bf-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e47bf-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e47bf-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e47bf-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e47bf-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e47bf-212">Testing single sign-on</span></span>

<span data-ttu-id="e47bf-213">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e47bf-213">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e47bf-214">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e47bf-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e47bf-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e47bf-215">Additional resources</span></span>

* [<span data-ttu-id="e47bf-216">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e47bf-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e47bf-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e47bf-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

