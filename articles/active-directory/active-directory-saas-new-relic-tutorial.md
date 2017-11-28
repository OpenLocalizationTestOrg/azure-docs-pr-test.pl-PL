---
title: "Samouczek: Integracji Azure Active Directory z usługi New Relic | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="44877-103">Samouczek: Integracji Azure Active Directory z usługi New Relic</span><span class="sxs-lookup"><span data-stu-id="44877-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="44877-104">Z tego samouczka, dowiesz się, jak toointegrate usługi New Relic w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44877-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44877-105">Integrowanie usługi New Relic z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44877-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44877-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="44877-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="44877-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNew Relic (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44877-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44877-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44877-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="44877-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44877-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44877-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44877-110">Prerequisites</span></span>

<span data-ttu-id="44877-111">tooconfigure integracji z usługą Azure AD z usługi New Relic należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44877-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="44877-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44877-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44877-113">Usługi New Relic logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44877-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44877-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44877-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44877-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44877-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44877-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44877-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44877-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44877-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44877-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44877-118">Scenario description</span></span>
<span data-ttu-id="44877-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44877-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44877-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44877-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44877-121">Dodawanie usługi New Relic w galerii hello</span><span class="sxs-lookup"><span data-stu-id="44877-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="44877-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44877-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="44877-123">Dodawanie usługi New Relic w galerii hello</span><span class="sxs-lookup"><span data-stu-id="44877-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="44877-124">tooconfigure hello integracji usługi New Relic w usłudze Azure Active Directory, należy tooadd usługi New Relic z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44877-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44877-125">**tooadd usługi New Relic w galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44877-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44877-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44877-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="44877-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44877-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44877-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44877-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="44877-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44877-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="44877-133">W polu wyszukiwania hello wpisz **usługi New Relic**.</span><span class="sxs-lookup"><span data-stu-id="44877-133">In hello search box, type **New Relic**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="44877-135">W panelu wyników hello, wybierz **usługi New Relic**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44877-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44877-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44877-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44877-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi New Relic w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="44877-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44877-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługi New Relic jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44877-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="44877-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi New Relic musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="44877-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="44877-141">Usługi New Relic, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="44877-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44877-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi New Relic, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="44877-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44877-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44877-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44877-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44877-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44877-145">**[Tworzenie użytkownika testowego usługi New Relic](#creating-a-new-relic-test-user)**  -toohave odpowiednikiem Simona Britta w usługi New Relic, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44877-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44877-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44877-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44877-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="44877-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44877-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44877-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44877-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="44877-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="44877-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi New Relic, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44877-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="44877-151">W portalu Azure na powitania hello **usługi New Relic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44877-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="44877-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44877-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="44877-155">Na powitania **adresy URL i nowej domeny Relic** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44877-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="44877-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="44877-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44877-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="44877-158">hello value is not real.</span></span> <span data-ttu-id="44877-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="44877-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="44877-160">Skontaktuj się z [zespołem pomocy technicznej nowego klienta Relic](https://support.newrelic.com/) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="44877-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="44877-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44877-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="44877-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44877-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44877-165">Na powitania **nowej konfiguracji Relic** kliknij **skonfigurować usługi New Relic** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="44877-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="44877-166">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="44877-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="44877-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **usługi New Relic** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44877-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="44877-169">W menu hello na górze hello, kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="44877-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="44877-170">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="44877-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="44877-171">Kliknij przycisk hello **zabezpieczeń i uwierzytelniania** , a następnie kliknij pozycję hello **jednokrotne** kartę.</span><span class="sxs-lookup"><span data-stu-id="44877-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="44877-172">![Logowanie jednokrotne](./media/active-directory-saas-new-relic-tutorial/ic797037.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="44877-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="44877-173">Na stronie okna dialogowego SAML hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44877-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="44877-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="44877-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="44877-175">a.</span><span class="sxs-lookup"><span data-stu-id="44877-175">a.</span></span> <span data-ttu-id="44877-176">Kliknij przycisk **wybierz plik** tooupload pobrany certyfikat usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44877-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="44877-177">b.</span><span class="sxs-lookup"><span data-stu-id="44877-177">b.</span></span> <span data-ttu-id="44877-178">W hello **adres URL logowania zdalnego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44877-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="44877-179">c.</span><span class="sxs-lookup"><span data-stu-id="44877-179">c.</span></span> <span data-ttu-id="44877-180">W hello **lądowanie adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44877-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="44877-181">d.</span><span class="sxs-lookup"><span data-stu-id="44877-181">d.</span></span> <span data-ttu-id="44877-182">Kliknij przycisk **Zapisz moje zmiany**.</span><span class="sxs-lookup"><span data-stu-id="44877-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="44877-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="44877-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44877-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="44877-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44877-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44877-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44877-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44877-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="44877-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="44877-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="44877-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44877-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44877-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44877-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44877-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44877-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44877-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44877-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44877-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44877-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44877-198">a.</span><span class="sxs-lookup"><span data-stu-id="44877-198">a.</span></span> <span data-ttu-id="44877-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44877-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44877-200">b.</span><span class="sxs-lookup"><span data-stu-id="44877-200">b.</span></span> <span data-ttu-id="44877-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44877-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44877-202">c.</span><span class="sxs-lookup"><span data-stu-id="44877-202">c.</span></span> <span data-ttu-id="44877-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="44877-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44877-204">d.</span><span class="sxs-lookup"><span data-stu-id="44877-204">d.</span></span> <span data-ttu-id="44877-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44877-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="44877-206">Tworzenie użytkownika testowego usługi New Relic</span><span class="sxs-lookup"><span data-stu-id="44877-206">Creating a New Relic test user</span></span>

<span data-ttu-id="44877-207">W przypadku użytkowników usługi Azure Active Directory toolog kolejności tooenable w tooNew Relic musi być przygotowana do usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="44877-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="44877-208">W przypadku hello usługi New Relic Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="44877-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="44877-209">**tooprovision tooNew konta użytkownika Relic, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44877-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="44877-210">Zaloguj się za tooyour **usługi New Relic** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44877-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="44877-211">W menu hello na górze hello, kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="44877-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="44877-212">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="44877-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="44877-213">W hello **konta** na powitania w okienku po lewej stronie, kliknij przycisk **Podsumowanie**, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="44877-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="44877-214">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="44877-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="44877-215">Na powitania **aktywni użytkownicy** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44877-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="44877-216">![Aktywni użytkownicy](./media/active-directory-saas-new-relic-tutorial/ic797042.png "aktywni użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="44877-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="44877-217">a.</span><span class="sxs-lookup"><span data-stu-id="44877-217">a.</span></span> <span data-ttu-id="44877-218">W hello **E-mail** pole tekstowe, hello typu adres e-mail z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision.</span><span class="sxs-lookup"><span data-stu-id="44877-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="44877-219">b.</span><span class="sxs-lookup"><span data-stu-id="44877-219">b.</span></span> <span data-ttu-id="44877-220">Jako **roli** wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="44877-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="44877-221">c.</span><span class="sxs-lookup"><span data-stu-id="44877-221">c.</span></span> <span data-ttu-id="44877-222">Kliknij przycisk **Dodaj tego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="44877-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="44877-223">Możesz użyć innych usługi New Relic użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez usługi New Relic tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="44877-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44877-224">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44877-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44877-225">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="44877-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="44877-227">**tooassign tooNew Simona Britta Relic, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44877-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="44877-228">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44877-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44877-230">Z listy aplikacji hello wybierz **usługi New Relic**.</span><span class="sxs-lookup"><span data-stu-id="44877-230">In hello applications list, select **New Relic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="44877-232">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44877-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="44877-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44877-234">Click **Add** button.</span></span> <span data-ttu-id="44877-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44877-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="44877-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44877-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44877-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44877-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44877-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44877-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44877-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44877-240">Testing single sign-on</span></span>

<span data-ttu-id="44877-241">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44877-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44877-242">Po kliknięciu kafelka usługi New Relic hello w hello Panel dostępu, należy pobrać aplikację usługi New Relic tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="44877-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44877-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44877-243">Additional resources</span></span>

* [<span data-ttu-id="44877-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44877-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44877-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44877-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

