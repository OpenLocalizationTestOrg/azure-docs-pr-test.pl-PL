---
title: 'Samouczek: Integracji Azure Active Directory z Projectplace | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="28a07-103">Samouczek: Integracji Azure Active Directory z Projectplace</span><span class="sxs-lookup"><span data-stu-id="28a07-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="28a07-104">Z tego samouczka, dowiesz się, jak toointegrate Projectplace w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28a07-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28a07-105">Integracja z usługą Azure AD Projectplace umożliwia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="28a07-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28a07-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooProjectplace</span><span class="sxs-lookup"><span data-stu-id="28a07-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="28a07-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooProjectplace (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a07-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28a07-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="28a07-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28a07-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28a07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28a07-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="28a07-110">Prerequisites</span></span>

<span data-ttu-id="28a07-111">tooconfigure integracji z usługą Azure AD z Projectplace należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="28a07-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="28a07-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28a07-113">Projectplace logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="28a07-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28a07-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="28a07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28a07-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="28a07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28a07-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="28a07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28a07-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28a07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28a07-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="28a07-118">Scenario description</span></span>
<span data-ttu-id="28a07-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="28a07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28a07-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="28a07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28a07-121">Dodawanie Projectplace z galerii hello</span><span class="sxs-lookup"><span data-stu-id="28a07-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="28a07-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="28a07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="28a07-123">Dodawanie Projectplace z galerii hello</span><span class="sxs-lookup"><span data-stu-id="28a07-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="28a07-124">tooconfigure hello integracji Projectplace do usługi Azure AD, należy tooadd Projectplace z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="28a07-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28a07-125">**tooadd Projectplace z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="28a07-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a07-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="28a07-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="28a07-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="28a07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28a07-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="28a07-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="28a07-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="28a07-133">W polu wyszukiwania hello wpisz **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="28a07-133">In hello search box, type **Projectplace**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="28a07-135">W panelu wyników hello zaznacz **Projectplace**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="28a07-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28a07-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="28a07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28a07-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Projectplace w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28a07-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Projectplace jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28a07-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="28a07-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Projectplace musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="28a07-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="28a07-141">W Projectplace, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="28a07-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="28a07-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Projectplace, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="28a07-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28a07-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="28a07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28a07-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="28a07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28a07-145">**[Tworzenie użytkownika testowego Projectplace](#creating-a-projectplace-test-user)**  -toohave odpowiednikiem Simona Britta w Projectplace, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28a07-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28a07-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="28a07-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28a07-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="28a07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28a07-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="28a07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28a07-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Projectplace.</span><span class="sxs-lookup"><span data-stu-id="28a07-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="28a07-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Projectplace, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="28a07-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a07-151">W portalu Azure na powitania hello **Projectplace** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="28a07-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="28a07-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="28a07-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="28a07-155">Na powitania **Projectplace domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28a07-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="28a07-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="28a07-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28a07-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="28a07-158">This value is not real.</span></span> <span data-ttu-id="28a07-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="28a07-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="28a07-160">Skontaktuj się z [zespołem pomocy technicznej klienta Projectplace](https://success.planview.com/Projectplace/Support) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="28a07-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="28a07-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="28a07-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="28a07-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="28a07-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="28a07-165">tooconfigure rejestracji jednokrotnej w **Projectplace** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="28a07-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="28a07-166">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="28a07-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="28a07-167">Witaj pojedynczego logowania jednokrotnego konfiguracja zawiera toobe wykonywane przez hello [zespołem pomocy technicznej Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="28a07-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="28a07-168">Otrzymasz powiadomienie, jak hello konfiguracji została ukończona.</span><span class="sxs-lookup"><span data-stu-id="28a07-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="28a07-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="28a07-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28a07-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="28a07-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28a07-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28a07-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28a07-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a07-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="28a07-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="28a07-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="28a07-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="28a07-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a07-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="28a07-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28a07-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="28a07-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28a07-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28a07-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="28a07-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28a07-184">a.</span><span class="sxs-lookup"><span data-stu-id="28a07-184">a.</span></span> <span data-ttu-id="28a07-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28a07-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28a07-186">b.</span><span class="sxs-lookup"><span data-stu-id="28a07-186">b.</span></span> <span data-ttu-id="28a07-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28a07-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28a07-188">c.</span><span class="sxs-lookup"><span data-stu-id="28a07-188">c.</span></span> <span data-ttu-id="28a07-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="28a07-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28a07-190">d.</span><span class="sxs-lookup"><span data-stu-id="28a07-190">d.</span></span> <span data-ttu-id="28a07-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="28a07-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="28a07-192">Tworzenie użytkownika testowego Projectplace</span><span class="sxs-lookup"><span data-stu-id="28a07-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="28a07-193">W kolejności tooenable usługi Azure AD użytkownicy toolog do Projectplace musi być przygotowana do Projectplace.</span><span class="sxs-lookup"><span data-stu-id="28a07-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="28a07-194">W przypadku hello Projectplace Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="28a07-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="28a07-195">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="28a07-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a07-196">Zaloguj się za tooyour **Projectplace** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="28a07-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="28a07-197">Przejdź za**osób**, a następnie kliknij przycisk **członków**.</span><span class="sxs-lookup"><span data-stu-id="28a07-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="28a07-198">![Osoby](./media/active-directory-saas-projectplace-tutorial/ic790228.png "osób")</span><span class="sxs-lookup"><span data-stu-id="28a07-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="28a07-199">Kliknij przycisk **dodać członka**.</span><span class="sxs-lookup"><span data-stu-id="28a07-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="28a07-200">![Dodawanie członków](./media/active-directory-saas-projectplace-tutorial/ic790232.png "dodawać członków")</span><span class="sxs-lookup"><span data-stu-id="28a07-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="28a07-201">W hello **dodać element członkowski** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="28a07-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="28a07-202">![Nowe elementy członkowskie](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nowych elementów członkowskich")</span><span class="sxs-lookup"><span data-stu-id="28a07-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="28a07-203">a.</span><span class="sxs-lookup"><span data-stu-id="28a07-203">a.</span></span> <span data-ttu-id="28a07-204">W hello **nowe elementy członkowskie** pole tekstowe, adres e-mail hello typu prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="28a07-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="28a07-205">b.</span><span class="sxs-lookup"><span data-stu-id="28a07-205">b.</span></span> <span data-ttu-id="28a07-206">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="28a07-206">Click **Send**.</span></span>

   <span data-ttu-id="28a07-207">Właściciel konta usługi Azure Active Directory toohello wysyłaniu wiadomości e-mail, zanim staje się aktywny w tym kontem hello tooconfirm łącza.</span><span class="sxs-lookup"><span data-stu-id="28a07-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="28a07-208">Możesz użyć innych Projectplace użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Projectplace tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="28a07-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28a07-209">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a07-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28a07-210">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooProjectplace.</span><span class="sxs-lookup"><span data-stu-id="28a07-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="28a07-212">**tooassign tooProjectplace Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="28a07-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a07-213">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="28a07-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="28a07-215">Z listy aplikacji hello wybierz **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="28a07-215">In hello applications list, select **Projectplace**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="28a07-217">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="28a07-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="28a07-219">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="28a07-219">Click **Add** button.</span></span> <span data-ttu-id="28a07-220">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="28a07-222">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="28a07-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28a07-223">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28a07-224">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="28a07-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28a07-225">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="28a07-225">Testing single sign-on</span></span>

<span data-ttu-id="28a07-226">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="28a07-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="28a07-227">Po kliknięciu kafelka Projectplace hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Projectplace aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28a07-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="28a07-228">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28a07-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28a07-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="28a07-229">Additional resources</span></span>

* [<span data-ttu-id="28a07-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28a07-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28a07-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28a07-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

