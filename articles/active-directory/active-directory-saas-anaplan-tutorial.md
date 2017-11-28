---
title: 'Samouczek: Integracji Azure Active Directory z Anaplan | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Anaplan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 38eb210d090e7aa720060680259124e941e30541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="fbf58-103">Samouczek: Integracji Azure Active Directory z Anaplan</span><span class="sxs-lookup"><span data-stu-id="fbf58-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="fbf58-104">Z tego samouczka, dowiesz się, jak toointegrate Anaplan w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbf58-104">In this tutorial, you learn how toointegrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbf58-105">Integracja z usługą Azure AD Anaplan zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fbf58-105">Integrating Anaplan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbf58-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAnaplan</span><span class="sxs-lookup"><span data-stu-id="fbf58-106">You can control in Azure AD who has access tooAnaplan</span></span>
- <span data-ttu-id="fbf58-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAnaplan (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf58-107">You can enable your users tooautomatically get signed-on tooAnaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbf58-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fbf58-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbf58-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbf58-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf58-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fbf58-110">Prerequisites</span></span>

<span data-ttu-id="fbf58-111">tooconfigure integracji z usługą Azure AD z Anaplan należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fbf58-111">tooconfigure Azure AD integration with Anaplan, you need hello following items:</span></span>

- <span data-ttu-id="fbf58-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbf58-113">Anaplan jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fbf58-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbf58-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbf58-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fbf58-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbf58-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fbf58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbf58-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbf58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbf58-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fbf58-118">Scenario description</span></span>
<span data-ttu-id="fbf58-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fbf58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbf58-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fbf58-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbf58-121">Dodawanie Anaplan z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fbf58-121">Adding Anaplan from hello gallery</span></span>
2. <span data-ttu-id="fbf58-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fbf58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-hello-gallery"></a><span data-ttu-id="fbf58-123">Dodawanie Anaplan z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fbf58-123">Adding Anaplan from hello gallery</span></span>
<span data-ttu-id="fbf58-124">tooconfigure hello integracji Anaplan do usługi Azure AD, należy tooadd Anaplan z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fbf58-124">tooconfigure hello integration of Anaplan into Azure AD, you need tooadd Anaplan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbf58-125">**tooadd Anaplan z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fbf58-125">**tooadd Anaplan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf58-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fbf58-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="fbf58-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbf58-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="fbf58-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="fbf58-133">W polu wyszukiwania hello wpisz **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-133">In hello search box, type **Anaplan**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="fbf58-135">W panelu wyników hello zaznacz **Anaplan**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fbf58-135">In hello results panel, select **Anaplan**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbf58-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fbf58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbf58-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Anaplan na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="fbf58-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbf58-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Anaplan jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf58-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Anaplan is tooa user in Azure AD.</span></span> <span data-ttu-id="fbf58-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Anaplan musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="fbf58-140">In other words, a link relationship between an Azure AD user and hello related user in Anaplan needs toobe established.</span></span>

<span data-ttu-id="fbf58-141">W Anaplan, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="fbf58-141">In Anaplan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbf58-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Anaplan, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="fbf58-142">tooconfigure and test Azure AD single sign-on with Anaplan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbf58-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fbf58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbf58-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fbf58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbf58-145">**[Tworzenie użytkownika testowego Anaplan](#creating-an-anaplan-test-user)**  -toohave odpowiednikiem Simona Britta w Anaplan, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fbf58-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - toohave a counterpart of Britta Simon in Anaplan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbf58-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fbf58-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbf58-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="fbf58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbf58-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fbf58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbf58-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Anaplan.</span><span class="sxs-lookup"><span data-stu-id="fbf58-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="fbf58-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Anaplan, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fbf58-150">**tooconfigure Azure AD single sign-on with Anaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf58-151">W portalu Azure na powitania hello **Anaplan** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-151">In hello Azure portal, on hello **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="fbf58-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fbf58-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="fbf58-155">Na powitania **Anaplan domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fbf58-155">On hello **Anaplan Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="fbf58-157">a.</span><span class="sxs-lookup"><span data-stu-id="fbf58-157">a.</span></span> <span data-ttu-id="fbf58-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="fbf58-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="fbf58-159">b.</span><span class="sxs-lookup"><span data-stu-id="fbf58-159">b.</span></span> <span data-ttu-id="fbf58-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="fbf58-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbf58-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="fbf58-161">These values are not real.</span></span> <span data-ttu-id="fbf58-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="fbf58-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbf58-163">Skontaktuj się z [zespołem pomocy technicznej klienta Anaplan](mailto:support@anaplan.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="fbf58-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="fbf58-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fbf58-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="fbf58-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fbf58-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbf58-168">Na powitania **konfiguracji Anaplan** kliknij **skonfigurować Anaplan** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="fbf58-168">On hello **Anaplan Configuration** section, click **Configure Anaplan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbf58-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="fbf58-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="fbf58-171">tooconfigure rejestracji jednokrotnej w **Anaplan** strony, należy pobrać hello toosend **XML metadanych**, **identyfikator jednostki SAML**, **SAML pojedynczy znak na adres URL usługi**  i **Sign-Out URL** za[zespołem pomocy technicznej Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="fbf58-171">tooconfigure single sign-on on **Anaplan** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   too[Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="fbf58-172">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="fbf58-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fbf58-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="fbf58-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbf58-174">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="fbf58-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbf58-175">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbf58-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbf58-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf58-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbf58-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="fbf58-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="fbf58-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fbf58-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf58-180">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fbf58-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbf58-182">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbf58-184">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbf58-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fbf58-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbf58-188">a.</span><span class="sxs-lookup"><span data-stu-id="fbf58-188">a.</span></span> <span data-ttu-id="fbf58-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbf58-190">b.</span><span class="sxs-lookup"><span data-stu-id="fbf58-190">b.</span></span> <span data-ttu-id="fbf58-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbf58-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbf58-192">c.</span><span class="sxs-lookup"><span data-stu-id="fbf58-192">c.</span></span> <span data-ttu-id="fbf58-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbf58-194">d.</span><span class="sxs-lookup"><span data-stu-id="fbf58-194">d.</span></span> <span data-ttu-id="fbf58-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="fbf58-196">Tworzenie użytkownika testowego Anaplan</span><span class="sxs-lookup"><span data-stu-id="fbf58-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="fbf58-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Anaplan.</span><span class="sxs-lookup"><span data-stu-id="fbf58-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="fbf58-198">We współpracy z [zespołem pomocy technicznej Anaplan](mailto:support@anaplan.com) tooadd hello użytkowników hello Anaplan platformy.</span><span class="sxs-lookup"><span data-stu-id="fbf58-198">Please work with [Anaplan support team](mailto:support@anaplan.com) tooadd hello users in hello Anaplan platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbf58-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf58-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbf58-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAnaplan.</span><span class="sxs-lookup"><span data-stu-id="fbf58-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnaplan.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="fbf58-202">**tooassign tooAnaplan Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="fbf58-202">**tooassign Britta Simon tooAnaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf58-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fbf58-205">Z listy aplikacji hello wybierz **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-205">In hello applications list, select **Anaplan**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="fbf58-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fbf58-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="fbf58-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fbf58-209">Click **Add** button.</span></span> <span data-ttu-id="fbf58-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="fbf58-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fbf58-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbf58-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbf58-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbf58-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbf58-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fbf58-215">Testing single sign-on</span></span>

<span data-ttu-id="fbf58-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fbf58-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbf58-217">Po kliknięciu kafelka Anaplan hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Anaplan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbf58-217">When you click hello Anaplan tile in hello Access Panel, you should get automatically signed-on tooyour Anaplan application.</span></span>

<span data-ttu-id="fbf58-218">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbf58-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fbf58-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fbf58-219">Additional resources</span></span>

* [<span data-ttu-id="fbf58-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbf58-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbf58-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbf58-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

